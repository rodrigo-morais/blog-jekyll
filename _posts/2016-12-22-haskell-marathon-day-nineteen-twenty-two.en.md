---
layout: post
title: Haskell's Marathon - Days Nineteen to Twenty Two
published: true
lang: en
translation: true
---

Hey folks!

Let’s start talking about *`Function Application`* operator which is a function that help us to remove parentheses from our functions. While *`Function Application`* with spaces are left-associative the *`Function Application`* with *`$`* is right-associative and because of that we can add functions without parentheses.

Function Application with spaces: f a b c => ((f a) b) c)  
Function Application with $: f a b c => (f (a (b c)))

<!--more-->

Let see some examples with *`Function Application`* operator:
```haskell
sqrt 3 + 2 * 5
1.732050807568877

sqrt (3 + 2 * 5)
3.605551275463989

sqrt $ 3 + 2 * 5
3.605551275463989
```
We can see here that *`$`* allowed us to remove the parentheses.

Another example:
```haskell
foldl (+) 0 (tail (map (*2) [1,2,3,4,5,6,7]))
54

foldl (+) 0 $ tail $ map (*2) [1,2,3,4,5,6,7]
54
```
In the second example we can remove all parentheses.

<br />

Now let’s take a look in *`Function Composition`* which is the way that we can can compose functions. *`Function Composition`* is represented by a *`.`* (point) in *`Haskell`*. Sometimes *`Function Composition`* allowed us to remove some parentheses as *`Function Application`*, but its principal responsibility is compose functions.
```haskell
map (\x -> negate (abs x)) [1,-2,3,-4,5,-6,7]
[-1,-2,-3,-4,-5,-6,-7]

map (negate .abs) [1,-2,3,-4,5,-6,7]
[-1,-2,-3,-4,-5,-6,-7]
```
See that we remove the anonymous function only leaving the function and we remove the parentheses. It happens because *`Function Composition`* just work with functions that are waiting for one parameter.

```haskell
sumTail :: (Num a, Ord a) => [a] -> [a] -> a
sumTail xs ys = foldl (+) 0 . tail . map (negate . abs) $ zipWith max xs ys

sumTail [1,2,3] [4,5,6]
-11
```
And we can combine *`Function Application`* with *`Function Composition`* and get clean and readable functions.
