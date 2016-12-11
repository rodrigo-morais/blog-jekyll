---
layout: post
title: Haskell's Marathon - Day Eleven - Part 1
published: true
lang: en
translation: true
---

Hey folks!


Yesterday we finished the first three chapters of the [book](http://learnyouahaskell.com/) which we are following. Today we will split our day in two steps. First step is to take a review of the first ten days and the second one is to do some exercises.


First, let’s take a quick review.
<!--more-->

<br />

**First Day**

The [first day](https://rodrigo-morais.github.io/haskell-marathon-day-one/) was about very basic introduction to *`Haskell`* and how to setup our environment. I think the most important here was the tip about use *`Docker`* because it makes our way easier. 
So install *`Docker`*, run this command docker run -ti --rm -v $(pwd):/code haskell:7.10 bash, and enjoy *`Haskell`*.
Beyond that we took a quick look in concepts as immutability, lazy, static types, arithmetics, boolean and functions.

<br />

**Second Day**

The [second day](https://rodrigo-morais.github.io/haskell-marathon-day-two/) we brought one the most important concepts in *`Haskell`* which is *`List`* and beyond that we talked about *`IF`* which is a simple and an niversal concept in development software world.
We saw some example of lists:
```haskell
let numbers = [1,2,3,4]
numbers
[1,2,3,4]
let words = [“car”,”ball”,”gremio”]
words
[“car”, “ball”, “gremio”]
```
And some about *`IF`* too.

<br />

**Third Day**

In the [third day](https://rodrigo-morais.github.io/haskell-marathon-day-three/) we dived more in the List subject.
We learnt some about nested lists, comparing lists and range of lists:
```haskell
-- Nested lists
[[1,2,3],[4,5,6]]
[[1,2,3],[4,5,6]]


[['h','e','l','l','o'],['w','o','r','l','d']]
["hello","world"]


-- Comparing lists
let listA = [1,2,3]
let listB = [1,2,3]
let listC = [1,3,4]


listA == listB
True


listA /= listB
False


listA == listC
False


listA >= listC
False


listA <= listC
True


-- Range of lists
[1..20]
[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]


['A'..'s']
"ABCDEFGHIJKLMNOPQRSTUVWXYZ[\\]^_`abcdefghijklmnopqrs"
```
We also take a look in other operators.

<br />

**Fourth Day**


During the [fourth day](https://rodrigo-morais.github.io/haskell-marathon-day-four/) we still talking about lists and we saw some content about *`Tuples`*.
First a quick look in the really important subject which is *`list comprehension`*.
```haskell
[ x*2 | x <- [1..10], x*2 > 10]
[12,14,16,18,20]
```
After a look how to use *`Tuples`* in *`Haskell`*.
```haskel
(1,2)
(1,2)
(1,2,”hello”)
(1,2,”hello”)
(1,2,”hello”, True)
(1,2,”hello”, True)
```
<br />

**Fifth Day**


The [fifth day](https://rodrigo-morais.github.io/haskell-marathon-day-five/) we studied what are *`static types`* in *`Haskell`* and the valid types which are *`Int`*, *`Integer`*, *`Float`*, *`Double`*, *`Bool`*, *`Char`* and *`Tuples`*.
We also took a look in how get the type of expressions, values and functions using the *`:t`*:
```haskell
:t ‘a’
‘a’ :: Char
:t True
True :: Bool
:t 5
5 :: Num a => a
let fnt x = x
fnt 4
4
fnt ‘a’
‘a’
:t fnt
fnt :: t -> t
```

<br />

**Sixth Day**


The [sixth day](https://rodrigo-morais.github.io/haskell-marathon-day-six/) was about *`type classes`* and that they are not classes. We took a look in the most important *`type classes`* in *`Haskell`*.

<br />

**Seventh Day**


The [seventh day](https://rodrigo-morais.github.io/haskell-marathon-day-seven/) was a different day. I went in a *`Haskell`* meetup where the group is following another [book](http://haskellbook.com/) and we worked with *`folds`*.

<br />

**Eight Day**


The [eight day](https://rodrigo-morais.github.io/haskell-marathon-day-eight/) was a really important one because we studyed *`Pattern Matching`*. This subject is really important and it  should be reviewed. Here an example:
```haskell
month' :: Int -> String
month' 5 = "May"
month' 6 = "June"
month' 7 = "July"
month' 8 = "August"
month' _ = "it is not a valid month"


month 5
"May"


month 6
"June"


month 7
"July"


month 9
"it is not a valid month"
```

<br />

**Ninth Day**


In the [ninth day](https://rodrigo-morais.github.io/haskell-marathon-day-nine/) we saw some other options to *`Pattern Matching`* as *`Guards`* and *`where`*:
```haskell
bmiStatus' :: Double -> Double -> String
bmiStatus' weight height
  | bmi <= 18.5 = "You are underweight!"
  | bmi <= 25 = "You are with ideal weight!"
  | bmi <= 30 = "You are overweight!"
  | otherwise = "You are obese!"
  where bmi = weight / height ^ 2


bmiStatus’ 85 1.81
"You are overweight!"


bmiStatus’ 80 1.81
"You are with ideal weight!"


bmiStatus’ 60 1.81
"You are underweight!"


bmiStatus’ 100 1.81
"You are obese!"
```

<br />

**Tenth Day**


The [last day](https://rodrigo-morais.github.io/haskell-marathon-day-ten/) we saw more options to *`Pattern Matching`* as *`let..in`* and *`case..of`*:
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
```
