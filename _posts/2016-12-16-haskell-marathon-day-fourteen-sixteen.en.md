---
layout: post
title: Haskell's Marathon - Days Fourteen, Fifteen and Sixteen
published: true
lang: en
translation: true
---

Hey folks!

First of all an explanation why I didn’t write separately posts to days fourteen, fifteen and sixteen. I realized that I was wasting too much time of my studies doing the posts and because of that I’ll try a new strategy to be more productive.

<!--more-->

## Fourteen

Ok. In the thirteenth day we talked about *`recursion`* and how it is important mainly in functional programming. Today let’s take a look in some standard functions which we can rewrite using *`recursion`*. The functions are *`replicate`*, *`take`*, *`reverse`*, *`repeat`*, *`zip`* and *`elem`*:

#### Replicate

Let’s start with *`replicate`* function which receive an Int and another value. The Int value is the quantity of times that the another value will be replicated.

```haskell
replicate' :: Int -> a -> [a]
replicate' 0 _ = []
replicate' n x = x : replicate' (n - 1) x

replicate' 5 3
[3,3,3,3,3]

replicate' 5 'a'
"aaaaa"
```
We can see that *`replicate`* function call itself till the Int value achive the number 0.

<br />

#### Take

The *`take`* function receives an Int which is the quantity and a list. The function should return a new list with the firsts elements from the received list according with the quantity informed.
```haskell
take' :: (Eq a) => Int -> [a] -> [a]
take' _ [] = []
take' n (x:xs)
  | n <= 0 = []
  | otherwise = x : take' (n - 1) xs

take’ 3 [1,2,3,4]
[1,2,3]

take’ 2 [1,2,3,4]
[1,2]
```

<br />

#### Reverse

The *`reverse`* function receives a list and return the same in the opposite order.

```haskell
reverse' :: [a] -> [a]
reverse' [] = []
reverse' (x:xs) = reverse' xs ++ [x]

reverse' [1,2,3,4,5]
[5,4,3,2,1]

reverse' ['a','b','c','d','e']
"edcba"
```

<br />

#### Repeat

The *`repeat`* function receives a value and repeat it infinitely.
```haskell
repeat' :: a -> [a]
repeat' x = x : repeat' x

take 10 $ repeat' 3
[3,3,3,3,3,3,3,3,3,3]

take 10 $ repeat' 'f'
"ffffffffff"
```

<br />

#### Zip

The *`zip`* function receives two lists and return a list of tuples combining them.
```haskell
zip' :: [a] -> [b] -> [(a,b)]
zip' _ [] = []
zip' [] _ = []
zip' (x:xs) (y:ys) = [(x,y)] ++ zip' xs ys

zip' [1,2,3] [6,7,8]
[(1,6),(2,7),(3,8)]

zip' ['a','b','c'] [6,7,8]
[('a',6),('b',7),('c',8)]

```

<br />

#### Elem

The *`elem`* function receives a value and a list and return a boolean to say if the value exist or not in the list.
```haskell
elem' :: (Eq a) => a -> [a] -> Bool
elem' _ [] = False
elem' x (y:ys)
  | x == y = True
  | otherwise = elem' x ys

3 [1,2,4,3,5,8,6]
True

elem' 7 [1,2,4,3,5,8,6]
False
```

All these previous functions are using *`recursion`* calling themselves to return the result.

<br />

Cool. Now let’s take a look in a function more complex. If you studied computer science you already worked with a *`Quick Sort`* function which receives unordered list, sort the list and return an ordered list.

Let’s take a look in its code:
```haskell
quickSort' :: (Ord a) => [a] -> [a]
quickSort' [] = []
quickSort' (x:xs) =
  let
    smaller = [ a | a <- xs, a < x ]
    bigger = [ a | a <- xs, a > x ]
    same = [ a | a <- xs, a == x ]
  in
    (quickSort' smaller) ++ [x] ++ same ++ (quickSort bigger)

quickSort [2,4,1,6,3,7,5,2,4]
[1,2,2,3,4,4,5,6,7]
```
This is a simple solution, we are picking the first element and checking what elements inside the list are smaller, equal or bigger. The smaller values will be in the left side of the element which we are evaluating and the elements with the same value or bigger will be on the right. The *`recursion`* is applied twice, one  to smaller and another to bigger elements. We are using *`let..in`* to make the function more readable.

<br />

## Fifteen

In the fifteenth day I study about *`higher-order function`* which is an important subject in functional programming and allow us to do much more things and give us much more power.  
We already saw some examples with *`higher-order function`* and it’s nothing more than pass a function as parameter to a function. The two most famous examples are the *`map`* and *`filter`* functions.  

 *`Map`* function receives a function as parameter and a list and apply the function to each element of the lsit returning a new one.
```haskell
map (*2) [1,2,3,4,5]
[2,4,6,8,10]

map (+2) [1,2,3,4,5]
[3,4,5,6,7]
```

<br />

The *`filter`* function receives a function which return a boolean and a list. The result of *`filter`* function is a new list with all elements from the old list which were applied to the function and returned True.
```haskell
filter (>= 3) [1,2,3,4,5,6]
[3,4,5,6]

filter (<= 3) [1,2,3,4,5,6]
[1,2,3]
```

<br />

Beyond the *`higher-order function`* I studied *`curried functions`* which is a function which receives always just one parameter and return a function. All functions in *`Haskell`* just receive one parameter. But we worked with a bunch of functions that received more than one parameter.  
How is it possible? *`Haskell`* uses *`curried functions`* to make it possible and provides a “syntax sugar” where we can work with multiples parameter.  
Let’s take a look:
```haskell
:t map
map :: (a -> b) -> [a] -> [b]

map (*2) [1,2,3,4,5]
[2,4,6,8,10]

let x = map (*2)
:t x
x :: Num b => [b] -> [b]

x [1,2,3,4,5]
[2,4,6,8,10]
```
Here we can see that. First we can see the type of *`map`* function which is: *`map :: (a -> b) -> [a] -> [b]`*  
If we run this expression *`map (*2) [1,2,3,4,5]`* we have this result *`[2,4,6,8,10]`*.  
What is happening? Firts *`Haskell`* is running just *`map`* function with the first parameter: *`map (*2)`* and returning a new function. And after running the new function with the second parameter. We did an example above using a variable to show it.

<br />

## Sixteen

In the sixteenth day I did some exercises to practice the *`higher-order function`* rewriting some *`Haskell`* standard functions as *`zipWith`*, *`flip`*, *`map`* and *`filter`*.

Below the *`map`* and *`filter`* rewrited.
```haskell
map' :: (a -> b) -> [a] -> [b]
map' _ [] = []
map' f (x:xs) = f x : map' f xs


filter' :: (a -> Bool) -> [a] -> [a]
filter' _ [] = []
filter' f (x:xs)
  | f x = x : filter' f xs
  | otherwise = filter' f xs
```

<br />

And I took a look in *`Lambda functions`* which are anonymous functions that we used just once.
```haskell
map (\x -> x + 3) [1,2,3,4]
[4,5,6,7]
```

The part of code above with this expression *`(\x -> x + 3)`* is the *`lambda function`*. I’ll write a post or posts about *`Lambda Functions`* because I think make easier understand *`functional programming`*.
