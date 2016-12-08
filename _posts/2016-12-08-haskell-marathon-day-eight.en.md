---
layout: post
title: Haskell's Marathon - Day Eight
published: true
lang: en
translation: true
---

Hey folks!

<br />

Today let’s talk about *`Pattern Matching`* one the best features in *`Functional Programming`* in my opinion.

As the majority functional languages *`Haskell`* has *`Pattern Matching`* which makes our lives much easier to create function with different actions depending what is received. *`Pattern Matching`* is about evaluate data and deconstruct them according those patterns.
The idea behind *`Pattern Matching`* is to make our program simpler and readable. Let’s dive in some examples and understand why.

<!--more-->

We can start with a function which receive a number and if this number is 5 then return the month “May” and if the number is different return the message “it is not a valid month”. How we implement that in a ordinary language?
```haskell
month :: Int -> String
month a =
  if a == 5 then
    "May"
  else
    "it is not a valid month"


month 5
“May”
month 6
"it is not a valid month"
```
Ok. A simple *`IF`* can solve the problem, but if we want get “June”, “July” and “August”?
```haskell
month :: Int -> String
month a =
  if a == 5 then
    "May"
  else if a == 6 then
    "June"
  else if a == 7 then
    "July"
  else if a == 8 then
    "August"
  else
    "it is not a valid month"


month 6
"June"
month 7
"July"
month 8
“August”
month 9
"it is not a valid month"
```
The *`IF`* solution still works, but it is pretty ugly. Imagine this function with all months.  
When we *`Pattern Matching`* a function we can create a body to each pattern making the function simpler and readable. Let’s see:
```haskell
month' :: Int -> String
month' 5 = "May"
month' 6 = "June"
month' 7 = "July"
month' 8 = "August"


month 5
"May"
month 6
"June"
month 7
"July"
month 8
“August”
month 9
"*** Exception: code/patter_matching.hs:(17,1)-(20,19): Non-exhaustive patterns in function month'
```
Much better than the *`IF`* version. What do you think?  
Pay attention that each month is a new function body.


Ok. But, where is the final *`ELSE`* to nonexistent months?  
Well, *`Pattern Matching`* has a feature called *`catchall`* which is the same than our final *`ELSE`*. In the example above we see the function failing because we don’t have the *`catchall`*.
```haskell
month' :: Int -> String
month' 5 = "May"
month' 6 = "June"
month' 7 = "July"
month' 8 = "August"
month' _ = "it is not a valid month"


month 9
"it is not a valid month"
```
Here to the *`catchall`* we are using an underscore (_) but we can use any other letter, symbol or word. Underscore is just a standard in *`Haskell`*.

Another important point is the order of functions. If we have the functions in incorrect order we can get a bug. In the month’s example if we have *`catchall`* before a month this month will never be called because *`catchall`* get all cases.
```haskell
month' :: Int -> String
month' 5 = "May"
month' _ = "it is not a valid month"
month' 6 = "June"
month' 7 = "July"
month' 8 = "August"


*Main> :l code/patter_matching.hs
[1 of 1] Compiling Main             ( code/patter_matching.hs, interpreted )


code/patter_matching.hs:17:1: Warning:
    Pattern match(es) are overlapped
    In an equation for ‘month'’:
        month' 6 = ...
        month' 7 = ...
        month' 8 = ...
Ok, modules loaded: Main.


month' 5
“May”
month' 6
"it is not a valid month"
month' 9
"it is not a valid month"
```


We can use *`Pattern Matching`* with *`Tuples`* too. If we want sum two *`Tuples`* how we can do?
```haskell
points :: (Int, Int) -> (Int, Int) -> (Int, Int)
points (a1, b1) (a2, b2) = (a1 + a2, b1 + b2)


points (2, 5) (7, 1)
(9,6)
```
In this case we don’t have *`catchall`* because the first pattern get all cases.
Another example with *`Tuples`* can be create a functions to triples. We already have the functions *`fst`* and *`snd`* to pairs, but we don’t have any function to triples. We can create then:
```haskell
first :: (a, b, c) -> a
first (a, _, _) = a


second :: (a, b, c) -> b
second (_, b, _) = b


third :: (a, b, c) -> c
third (_, _, c) = c


first (1,2,3)
1
second (1,2,3)
2
third (1,2,3)
3


``` 


And the most important we can use *`Pattern Matching`* with lists which probably where we will use the most this technic. We saw before the functions *`head`* and *`tail`* which we can use with lists. Let’s rewrite them:
```haskell
head' :: [a] -> a
head' (x:_) = x


tail' :: [a] -> [a]
tail' (_:xs) = xs


head' [1,2,3]
1
tail' [1,2,3]
[2,3]


head' []
*** Exception: code/patter_matching.hs:39:1-15: Non-exhaustive patterns in function head'


tail' []
*** Exception: code/patter_matching.hs:42:1-17: Non-exhaustive patterns in function tail'
``` 
Here we can see that the functions are working when they receive a list with elements, but when the list is empty the functions are breaking. Let’s solve it.


```haskell
head' :: [a] -> a
head' [] = error "list is empty"
head' (x:_) = x


tail' :: [a] -> [a]
tail' [] = [


head' [1,2,3]
1


tail' [1,2,3]
[2,3]


head' []
*** Exception: list is empty


tail' []
[]
```
Now is everything working, we gave two different solutions to each function. To *`head`* we are calling an error when we receive an empty list because we don’t have element to return, on the other hand to *`tail`* we are returning an empty list when we receive an empty list because the rest of nothing is nothing.


Beyond that we have a curiosity in this implementation, we can see that in *`head`* function we are receiving the list as *`(x:_)`* and in *`tail`* function as *`(_:xs)`*. It happens because in *`Haskell`* we can represent a list as *`x:xs`* where *`x`* is the first element and *`xs`* is the rest.
One example is the list *`[1,2,3,4]`* which can be represented as *`(1:(2:(3:(4))))`*. In this case *`1`* is *`x`* and *`(2:(3:(4)))`* is *`xs`*.

<br />

*`Pattern Matching`* is a super feature to *`Functional Programming`* because makes the code simpler and readable. I can say that is my favorite feature. Prepare yourself because you will work a lot with *`Pattern Matching`* when you are using *`Functional Programming`*.
