---
layout: post
title: Haskell's Marathon - Day Twelve
published: true
lang: en
translation: true
---

Hey folks!


Today we still working with some exercises. Yesterday we did some exercises and in the exercise number nine we use two standard functions from *`Haskell`* which were *`takeWhile`* and *`dropWhile`*. Now we will do something slightly different we will create our *`takeWhile`* and *`dropWhile`* and use it in exercise nine.


<!--more-->


Let’s start with *`takeWhile`* because after the *`dropWhile`* will be pretty similar.
The function *`takeWhile`* gets the elements from a list while them are respecting the function informed.
```haskell
takeWhile (=='a') ['a', 'a', 'a', 'a', 'b', 'c', 'c', 'a', 'a', 'd', 'e', 'e', 'e', 'e']
"aaaa"


takeWhile (<= 3) [1,2,3,4,5,6]
[1,2,3]
```
Ok. When we want create a function is always easier start thinking in its behavior. In *`Haskell`* we do that thinking in the function’s signature.  
How is the *`takeWhile`* signature? Well, it receives a function and a list. The result is a list.  
Ok, and how is the function? The function receive an element and return a boolean.  
Great, looks like we already have a signature.
```haskell
takeWhile’ :: (a -> Bool) -> [a] -> [a]
```
The *`(a -> Bool)`* is our function which receive an element *`a`* and return a boolean. *`[a]`* is the list which we receive and the last *`[a]`* is the list which we return.


Cool. The next step is think about exceptions which in our case is when we receive an empty list. What we can do with an empty list? Nothing. Then let’s write it:
```haskell
takeWhile’ :: (a -> Bool) -> [a] -> [a]
takeWhile’ _ [] = []
```
In this case the function is not important and we are using *`_`* to it.  
Now to the most important part of our function. Let’s think, what happens when the first element of the list is true to our function? In this case we want to return it and still evaluating the list.
```haskell
takeWhile’ :: (a -> Bool) -> [a] -> [a]
takeWhile’ _ [] = []
takeWhile’ f (x:xs) =
    If f x then
        x: takeWhile’ f xs
```
Simple like that.


Ok. But when the function returns false to our element? Well, in this case we have to not return the element and stop with the list evaluation.
```haskell
takeWhile’ :: (a -> Bool) -> [a] -> [a]
takeWhile’ _ [] = []
takeWhile’ f (x:xs) =
    If f x then
        x: takeWhile’ f xs
    else
        []
```
And if we test:
```haskell
takeWhile’ (=='a') ['a', 'a', 'a', 'a', 'b', 'c', 'c', 'a', 'a', 'd', 'e', 'e', 'e', 'e']
"aaaa"


takeWhile’ (<= 3) [1,2,3,4,5,6]
[1,2,3]
```
Works. But we can improve the function using *`Guards`*. Let’s try?
```haskell
takeWhile'' :: (a -> Bool) -> [a] -> [a]
takeWhile'' _ [] = []
takeWhile'' f (x:xs)
  | f x = x : takeWhile' f xs
  | otherwise = []


takeWhile’’ (=='a') ['a', 'a', 'a', 'a', 'b', 'c', 'c', 'a', 'a', 'd', 'e', 'e', 'e', 'e']
"aaaa"


takeWhile’’ (<= 3) [1,2,3,4,5,6]
[1,2,3]
```
Works too. And the function looks better. What do you think?




Ok. Now let’s see the *`dropWhile`* function. This function receives as parameter a function and a list and returns another list. Similar to *`takeWhile`*, is not?
And there is more, if the list received is empty it will return an empty list too.
```haskell
dropWhile’ :: (a -> Bool) -> [a] -> [a]
dropWhile’ _ [] = []
```
What will change in *`dropWhile`* is the last part which has a different behaviour than *`takeWhile`*. In *`dropWhile`* we want remove the element if it is true to the function received as parameter. And if the element is false we stop with the evaluation of the list and return it with the element.
```haskell
dropWhile'' :: (a -> Bool) -> [a] -> [a]
dropWhile'' _ [] = []
dropWhile'' f (x:xs)
  | f x = dropWhile' f xs
  | otherwise = x:xs


dropWhile'' (<= 3) [1,2,3,4,5,6]
[4,5,6]


dropWhile'' (=='a') ['a', 'a', 'a', 'a', 'b', 'c', 'c', 'a', 'a', 'd', 'e', 'e', 'e', 'e']
"bccaadeeee"
```
Works too.


Now we can return to exercise nine which we worked yesterday and replace the standard functions for our functions.


The description of exercise is: Pack consecutive duplicates of list elements into sublists. If a list contains repeated elements they should be placed in separate sublists.


And this is the example:
```haskell
pack ['a', 'a', 'a', 'a', 'b', 'c', 'c', 'a',  'a', 'd', 'e', 'e', 'e', 'e']
["aaaa","b","cc","aa","d","eeee"]
```
With our new functions:
```haskell
pack :: (Eq a) => [a] -> [[a]]
pack [] = []
pack (x:xs) = (x: takeWhile’’ (==x) xs) : (pack $ dropWhile’’ (==x) xs)


pack ['a', 'a', 'a', 'a', 'b', 'c', 'c', 'a',  'a', 'd', 'e', 'e', 'e', 'e']
["aaaa","b","cc","aa","d","eeee"]
```
And the *`pack`* function still working with our functions.

<br />

To rewrite the functions *`takeWhile`* and *`dropWhile`* we had to use two techniques called *`recursion`* and *`high order function`* which we will study in the next two chapters of the [book](http://learnyouahaskell.com/) that we are following.
