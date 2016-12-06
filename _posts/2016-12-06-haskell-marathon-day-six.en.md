---
layout: post
title: Haskell's Marathon - Day Six
published: true
lang: en
translation: true
---

Hey folks!


Yesterday we understand how types work in *`Haskell`*, what types *`Haskell`* supports and that we have type variables which can help us a lot.
Today let’s talk about *`type classes`*. First of all we have to say that *`type classes`* are not classes. With this disclaimer we can go ahead and discover what hell type classes are.


<!--more-->


*`Type class`* is not more than an interface which describe some behaviour. If a type is an instance from a type class, then it implements this behaviour.
To be more clear, *`type class`* is just a collection of functions which we decide what they mean for the type.
The most common type classes in *`Haskell`* are *`Eq`*, *`Ord`*, *`Show`*, *`Read`*, *`Enum`*, *`Bounded`*, *`Num`*, *`Floating`* and *`Integral`*. Let’s give a quick summary to each one.

<br />

**Eq type class**

First let’s check the type of *`==`* operator which is an instance of *`Eq`*.
```haskell
:t (==)
(==) :: Eq a => a -> a -> Bool
```
How we already know the *`:t`* return the type from a value and function. The operator *`==`* is a function and we can see its types. We already learnt how read it. The function receives two types variable called “a” and return a *`Bool`*. But wait a minute, what hell is *`Eq a =>`*? *`Eq a =>`* wants say that the type “a” should be an instance of *`Eq`* class.
The *`Eq`* *`type class`* provide an interface for testing for equality. If it makes sense for two items from a determined type we can say that they are an instance of *`Eq`*. Almost all standard *`Haskell`* types are instances of *`Eq`*.
*`Eq`*’s instances implement two functions which are *`==`* and *`/=`*.

<br />

**Ord type class**

*`Ord`* is a *`type class`* for types whose values can be put in some order.  Let’s take a look in a operator to *`Ord`* *`type class`*:
```haskell
:t (<)
(<) :: Ord a => a -> a -> Bool
5 < 6
True
5 < 4
False
```
The type *`<`* is similar to *`==`* which we saw before. All the types we’ve cover so far are instances of *`Ord`* just functions are not. The operators to *`Ord`* are *`<`*, *`<=`*, *`>`* and *`>=`*.

<br />

**Show type class**

Types which are instances of *`Show`* *`type class`* can be represented as strings. As *`Ord`*, all types that we covered are instances of *`Show`* *`type class`* just functions are not. The behaviour from *`Show`* *`type class`* is print the values.
```haskell
show 5
"5"
show 'a'
"'a'"
show True
"True"
```

<br />

**Read type class**

The behaviour from *`Read`* *`type class`* is the opposite of the behaviour from *`Show`* *`type class`*, but all the rest are the same. It reads a string and transformss in a value.
```haskell
read "True" || False
True
read "True" && False
False
read "5" + 4
9
read "['a']" ++ ['h']
"ah"
```

<br />

**Enum type class**

*`Enum`* *`type class`* has the behaviour to make sequences. So all instances from *`Enum`* *`type class`* are sequentially ordered types and the values can be enumerated. These instances can be used in list ranges and have successor and predecessor.
```haskell
['a'..'f']
"Abcdef"
[3..9]
[3,4,5,6,7,8,9]
```

<br />

**Num type class**

*`Num`* is a numeric *`type class`*. Its instances can act as numbers.
```haskell
:t 5
5 :: Num a => a
5 :: Int
5
5 :: Integer
5
5 :: Float
5.0
5 :: Double
5.0
```

<br />

**Floating type class**

*`Floating`* *`type class`* has as instances the types *`Float`* and *`Double`*. The functions which are instances of *`Floating`* *`type class`* must represent floating-point.
```haskell
sin 2
0.9092974268256817
cos 2
-0.4161468365471424
```

<br />

**Integral type class**

*`Integral`* *`type class`* is another numeric *`type class`* which includes *`Int`* and *`Integer`*.

<br />

A type can be instance of multiplies *`type classes`*. We have to think, that as an interface, each *`type class`* gives to a type behaviours which have to be followed. For example, a type can be an instance of *`Eq`* type class and *`Ord`* type class and have the equality behaviour and ordening behaviour.
Looks like that *`type classes`* are not so useful to us right now, but in more complex stuff of *`Haskell`* this knowledge will help us.
