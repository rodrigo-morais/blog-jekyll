---
layout: post
title: Haskell's Marathon - Day Ten
published: true
lang: en
translation: true
---

Hey folks!


Today we will talk about two different options to work with *`Pattern Matching`* which are *`let..in`* and *`case..of`*.


We already saw a little bit about *`let..in`* in the first day where we are using it to create variables’ *`GHCI`*, but we can use it a slightly different.
<!--more-->
```haskell
let a = 5
5 * 5
25


let add a b = a + b
add 5 4
9


let add' a b = a + b in add' 5 4
9
```


Instead of use *`where`* we can use *`let..in`* and put the “variables” on the top.
```haskell
cylinder :: Double -> Double -> Double
cylinder r h =
  let
    sideArea = 2 * pi * r * h
    topArea = pi * r ^ 2
  in
    sideArea + 2 * topArea


cylinder 8 10
904.7786842338604
```
Different of *`where`* the *`let..in`* is an expression and can be used everywhere, on the other hand it has scope just where it is defined and we can't use with *`Guards`* for example. Let’s see an example where we can use *`let..in`*.
```haskell
4 + let b = 5 in 5 + b + 2


[let square x = x * x in (square 2, square 3, square 4)]
[(4,9,16)]
```
When we say that *`let..in`* is an expression we want to say that it has a value and because of that we can use it everywhere.


We can use *`let..in`* in list comprehension too. With *`let..in`* in list comprehensions we can create variables which can be used in the output and everything comes after the *`let..in`* definition.
```haskell
calcBMI :: [(Double, Double)] -> [Double]
calcBMI xs = [bmi | (weight, height) <- xs, let bmi = weight / height ^ 2]


calcBMI [(85, 1.81), (70, 1.9), (60, 1.5), (90, 1.8)]
[25.94548395958609,19.390581717451525,26.666666666666668,27.777777777777775]


getOverweight :: [(Double, Double)] -> [Double]
getOverweight xs = [bmi | (weight, height) <- xs, let bmi = weight / height ^ 2, bmi > 25.0]


getOverweight [(85, 1.81), (70, 1.9), (60, 1.5), (90, 1.8)]
[25.94548395958609,26.666666666666668,27.777777777777775]
```
In this case we don’t need auxiliary functions to our list comprehension.


*`Haskell`* has a different way to do *`Pattern Matching`* which is *`case..of`*. Both doing the same, but as an expression *`case..of`* can be used anywhere and *`Pattern Matching`* can’t.
```haskell
head' :: [a] -> a
head' xs = case xs of
  [] -> error "empty list"
  (x:_) -> x


head' []
*** Exception: empty list


head' [1]
1


head' [1,2]
1


listType :: [a] -> String
listType xs = "This is " ++ case xs of
  [] -> "an empty list"
  [a] -> "list with a single element"
  _ -> "a list with more than one element"


listType []
"This is an empty list"


listType [1]
"This is list with a single element"


listType [1,2]
"This is a list with more than one element"
```
With *`case..of`* we can create a function as *`Pattern Matching`* or add it inside the other expression.

<br />

Today we saw other possibilities to work with list and sometimes not use *`Pattern Matching`*. With these content we finalized the third chapter of book “Learn You a Haskell for Great Good!: A Beginner’s Guide”.
