---
layout: post
title: Haskell's Marathon - Day Five
published: true
lang: en
translation: true
---

Hey folks!


What is your type?
Today we will understand, or try, a little bit how the type system works in *`Haskell`*.


In *`Haskell`* everything has a type and they are validate in compile time. It makes the code safer because the errors are catched soon and not during the execution.
Unlike other languages as *`Java`* and *`C#`*, *`Haskell`* has type inference. It means that we don’t need say to *`Haskell`* what type each element is, and our code doesn’t become verbose.

<!--more-->

If *`Haskell`* is a statically typed language we have to have one way to get the types from functions and values. For to do that we can use *`:t`* which give us the type from a value or function. Let’s see:


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
The operator *`::`* is called “has type of” and the explicit types are always denoted with the first letter in uppercase.
One thing which is important is the function, which return a type different. The type from function means that the function *`fnt`* will receive a type *`t`* and return a type *`t`* where *`t`* can be any valid type to *`Haskell`*.


But what are the valid types to *`Haskell`*?
We can start saying that *`Haskell`* has two types to integers which are *`Int`* and *`Integer`*. The difference is that *`Integer`* type is used to big numbers.


```haskell
factorial :: Int -> Int
factorial n = product [1..n]


factorial' :: Integer -> Integer
factorial' n = product [1..n]


factorial 25
7034535277573963776


factorial’ 25
15511210043330985984000000
```


To floating-point *`Haskell`* has two types. *`Float`* is to single precision and *`Double`* to double the precision. *`Char`* and *`Bool`* are types too. And *`Tuple`* which we saw before are types too, it depends of their length and the type of their components.


*`Haskell`* has something called type variables, which is relationated with the function type example that we saw some lines above. Sometimes one function doesn’t have a defined type and we use a type variable to define it. Type variable in Haskell can be any word, but usually are used one character as ‘a’ or ‘b’. Let’s take a look in the function *`head`* which get the first element from a list.
```haskell
head [1,2,3,4]
1
head [‘h’,’e’,’l’,’l’,’o’]
‘h’
:t head
head :: [a] -> a
```
As we can see the type of *`head`* is a list of any type that return an element of same type.
Type variables are pretty cool because they give us some freedom when we don’t want create a strict rule for a function or when our function can handle with different types. This behaviour / feature is like what other languages call generics.


Today we understand a little how *`Haskell`* handles with types. Tomorrow we will take a look in *`type classes`* and see that they are not classes.
