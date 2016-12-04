---
layout: post
title: Haskell's Marathon - Day Two
published: true
lang: en
translation: true
---

Today is my second day in *`Haskell’s`* marathon and we will talk about conditional with IF and lists.


**Conditional (IF)**

In *`Haskell`* as other languages we can use conditionals to produce more interesting functions. One the most famous conditional is *`IF`* which we can test values and return new values following this test. The biggest difference between *`Haskell`* and other languages is that *`Haskell`* forbids us that use *`IF`* without *`ELSE`*. It happens because in *`Haskell`* all functions have to have a return and if we have an *`IF`* clause without *`ELSE`* we can doesn’t have any return in a function.
Let’s take a look in some examples using *`IF`* clause:
```haskell
let biggerThanTen x = if x > 10 then "BIGGER" else "SMALLER"
biggerThanTen 5
SMALLER
biggerThanTen 12
BIGGER
let isOdd x = if x `mod` 2 == 0 then False else True
isOdd 2
False
isOdd 3
True
isOdd 4
False
isOdd 5
True
```
<br />

**Lists**

In *`Haskell`* lists are an homogeneous data structure, it means that which list accept always the same type. We can’t mix numbers and strings in the same list.
To create a list we put the elements inside brackets as:
```haskell
let numbers = [1,2,3,4]
numbers
[1,2,3,4]
let words = [“car”,”ball”,”gremio”]
words
[“car”, “ball”, “gremio”]
```
Probably one the most important functions / actions when we are using lists is concatenations. We have some different forms of concatenate lists.
Let’s take a look!
```haskell
[1,2,3] ++ [4,5,6] -- ++ is used to concatenate two list and have a new list from this union
“hello” ++ “ “ ++ “world”
“hello world”
1 : [2,3,4,5] -- : is used to add a new element in the beginning of the list 
[1,2,3,4,5]
‘A’ : “pple”
“Apple”
```

Another important function with list is get an element by position. To do this we have to use *`!!`* which allows us get the element.
```haskell
[3,5,2,4,1] !! 3
4
[‘h’,’e’,’l’,’l’,’o’] !! 2
‘l’
[‘h’,’e’,’l’,’l’,’o’] !! 9
*** Exception: Prelude.!!: index too large
```
In this example we can see two important facts about lists in *`Haskell`*. First one is that all lists start with index 0, and the second one is that if we try get an index which doesn’t exist we will receive an error as result.

<br />

Today we took a look in *`IF`* conditional and lists. Tomorrow we will continue taking a look in list and what we can do with.
