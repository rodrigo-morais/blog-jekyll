---
layout: post
title: Haskell's Marathon - Day Thirteen
published: true
lang: en
translation: true
---

Hey folks!


Yesterday we rewrote some standard functions from *`Haskell`* and how I commented these functions was using *`recursion`*.
Probably the majority or totality of your know what *`recursion`* is. But if by chance someone doesn’t know I’ll try explain in few words.


<!--more-->


*`Recursion`* is or happens when a function calls itself with a different parameter until find a base case. And what is a base case? Base case is a case where the function return a result and doesn’t call itself, with other words when the functions doesn't have more work for to do.


A good example for *`recursion`* is *`fibonacci`*.  
How is it works? Well, let’s start thinking in *`fibonacci`* signature which is a function receives a number and return a list. So *`fibonacci`* receives a number and decomposes this list until achieve the number 1. Each step the number decreases one. If the number is 1 or 0 it returns the same number in a list. Ops, 1 or 0? Looks like we found our base cases.
Let’s see an example:


If *`fibonacci`* receives the number 4, how is it work?  
4 : 3 : 2 : 1 = [4,3,2,1]
Let’s look that in other prism.
4 + (4 - 1) + ((4 - 1) - 1) + ((4 - 1) - 1) - 1) = [4,3,2,1]
Can you see the *`recursion`* in this last example? No, neither I.
Let’s see how is the function in *`Haskell`*:
```haskell
fibonacci :: Int -> [Int]
fibonacci 0 = [0]
fibonacci 1 = [1]
fibonacci x = x : fibonacci (x - 1)


fibonacci 4
[4,3,2,1]
```
Now you can see the *`recursion`* and the *`fibonacci*` function calling itself.


<br />


In functional programming the *`recursion`* technique is really important, unlike the imperative programming we don’t have steps to follow and because of that the function has to call itself to return some valuable data or for to do something interesting.
