---
layout: post
title: Haskell's Marathon - Days Seventeen and Eighteen
published: true
lang: en
translation: true
---

Hey folks!

These last days I studied about *`folds`* and *`scans`*. 
 
So today let’s start talking about *`folds`* which are the same than *`reducers`* in other languages. *`Haskell`* has two kind of *`folds`* which are *`foldl`* and *`foldr`*.

<!--more-->

### foldl

*`foldl`* function is used when we want start to *`fold`* a list from left to right. For example if we have a list as [1,2,3,4,5] in *`foldl`* function we will do this process:  
(((((0 + 1) + 2) + 3) + 4) + 5) => ((((1 + 2) + 3) + 4) + 5) => (((3 + 3) + 4) + 5) => ((6 + 4) + 5) => (10 + 5) => 15

The *`foldl`* function has this signature *`foldl :: (b -> a -> b) -> b -> [a] -> b`* which is saying to us that we will receive a function, an element with any type, a list and we it will return one element as result.  
The function will be applied over the list and the second element is the accumulator.  
Let’s see how it works:
```haskell
foldl (+) 0 [1,2,3,4,5]
15

foldl (*) 3 [1,2,3,4,5]
360
```
Then in the first example we saw that the function received was *`(+)`*, the accumulator was *`0`* and the list was *`[1,2,3,4,5]`*. The result was *`15`* as we simulated before.

I rewrote the *`foldl`* function and it was like that:
```haskell
foldl' :: (b -> a -> b) -> b -> [a] -> b
foldl' _ acc [] = acc
foldl' f acc (x:xs) = foldl' f (f acc x) xs

foldl' (+) 0 [1,2,3,4,5]
15

foldl' (*) 3 [1,2,3,4,5]
360
```

<br />

### foldr
*`foldr`* function is similar to *`foldl`* but it does the computation from right to left. Let’s see an example with a sum in a list [1,2,3,4,5]:  
(1 + (2 + (3 + ( 4 + (5 + 0))))) => (1 + (2 + (3 + ( 4 + 5)))) => (1 + (2 + (3 + 9))) => (1 + (2 + 12)) => (1 + 14) => 15

The signature to *`foldr`* function is *`foldr :: (a -> b -> b) -> b -> [a] -> b`*.  
Let’s see some examples:
```haskell
foldr (+) 0 [1,2,3,4,5]
15

foldr (*) 3 [1,2,3,4,5]
360
```
Just the same than *`foldl`* function.  
 The *`foldr`*  shine when is used to concatenate lists or in infinite lists. With list concatenation because the operation *`:`* is much cheaper than *`++`* to concatenation of lists, and the majority of time we will use *`foldr`* and *`:`* or *`foldl`* and *`++`*. About infinite lists because in some infinite lists *`foldl`* doesn’t work when *`foldr`* still working. It is happens because *`foldr`* doesn’t need process all list to evaluate it taking advantage from *`Haskell`* laziness.  
Below the code to rewrite the *`foldr`* function.
```haskell
foldr'' :: (a -> b -> b) -> b -> [a] -> b
foldr'' _ acc [] = acc
foldr'' f acc (x:xs) =
  f x (foldr'' f acc xs)
```

To see the difference between *`foldl`* and *`foldr`* we have use functions to divide or subtract values. Let’s do that:
```haskell
foldl (-) 100 [54,20]
26

foldr (-) 100 [54,20]
134
```
Here *`foldl`* function compute the values in this order *`((100 - 54) - 20)`* and *`foldr`* in this order *`(54 - (20 - 100))`* and because that the results are different.  
Another example with division:
```haskell
foldl (/) 100 [5,2]
10.0

foldr (/) 100 [5,2]
250.0
```
The same idea which we saw before.

<br />

### Scan

Now let’s take a quick look in another function called *`scan`*. It does the same that *`fold`* but the result is not just one value but a list. The list has all accumulators created during the computation. *`Scan`* has two function as *`fold`* which are *`scanl`* and *`scanr`*.
Let’s compare *`scan`* and *`fold`*:
```haskell
foldl (/) 100 [5,2]
10.0

scanl (/) 100 [5,2]
[100.0,20.0,10.0]

foldr (/) 100 [5,2]
250.0

scanr (/) 100 [5,2]
[250.0,2.0e-2,100.0]
```

Can you see? We have the same final result, but *`scan`* brought all accumulators which were computed. In *`scanl`* function we have the result in the end of the list and in *`scanr`* in the head.
