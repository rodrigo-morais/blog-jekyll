---
layout: post
title: Haskell’s marathon - Day Fifty Four to Fifty Five
published: true
lang: en
translation: false
---

Hey folks!

Today we will take a look in *`type classes`* which we already learnt in the first posts. Now we will see how to use them.

<br />

**What are *`Type Classes`***

How we already saw *`type classes`* are not *`classes`* as in *`Object Oriented`* languages. We can use than as a sort of interfaces to reuse some functionalities in types which we are creating.  
There are some *`type classes`* that we already took a look as *`Eq`*, *`Ord`*, *`Show`* and etc.
<!--more-->

<br />

***`Eq type class`***

Let’s start creating a type and deriving the *`type class Eq`* to it.
```haskell
data Person = Person {
  firstName :: String,
  lastName :: String,
  age :: Int
} deriving (Eq)

let rodrigo = Person { firstName = "Rodrigo", lastName = "Morais", age = 37 }
let rodrigo1 = Person { firstName = "Rodrigo", lastName = "Morais", age = 37 }
let sybila = Person { firstName = "Sybila", lastName = "Esteves", age = 32 }
```
So we created a type called *`Person`* and some values to it. When a person has the same first, last name and age in two different instances they are the same.  
Let’s test:
```haskell
> rodrigo == rodrigo1
True

> rodrigo /= rodrigo1
False

> rodrigo /= sybila
True

> rodrigo == sybila
False

> rodrigo1 == sybila
False

> rodrigo1 /= sybila
True
```
Here we can see that *`rodrigo`* and *`rodrigo1`* are the same person, but *`sybila`* is different to them.

<br />

***`Show type class`***

So let’s say that we want to print on the screen the people which we created before.
```haskell
> rodrigo

<interactive>:16:1:
    No instance for (Show Person) arising from a use of ‘print’
    In a stmt of an interactive GHCi command: print it
```
When we try it *`Haskell`* uses the function *`Show`*, but our type does have this function. This function is part of the *`Show type class`* then let’s derive it in our type:
```haskell
data Person = Person {
  firstName :: String,
  lastName :: String,
  age :: Int
} deriving (Eq, Show)
```
Now our type is deriving the *`type classes Eq `* and *`Show`*. And because of that we can print our people on the screen.
```haskell
> rodrigo
Person {firstName = "Rodrigo", lastName = "Morais", age = 37}
``` 

<br />

Today we made a review about what *`type classes`* are and saw how to use them. *`Type Classes`* are important to reuse code in *`Haskell`*.
