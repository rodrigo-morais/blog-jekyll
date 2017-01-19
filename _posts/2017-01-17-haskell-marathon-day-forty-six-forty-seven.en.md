---
layout: post
title: Haskell’s marathon - Day Forty Six to Forty Seven
published: true
lang: en
translation: false
---

Hey folks!

Last posts we talked about modules. Now we are in the seventh chapter from the [book](http://learnyouahaskell.com/) which we are following and we’ll start to talk about how create our own data types.  

<br />

**Standard Types**

First let’s see how *`Haskell`* creates the types in standard library. We can see a simple type as *`Boolean`*:
```haskell
data Boolean = True | False
```
<!--more-->
This line wants to say that we are creating a type *`Boolean`* with two value constructors. One value constructor is *`True`* and another is *`False`*. The character *`|`* is read as or. So we have value constructor as *`True`* or *`False`*. The *`data`* keyword means a new type.  
Both the type name which is *`Boolean`* here and the value constructors which are *`True`* or *`False`* must start with uppercase letter.

<br />

**Our own Data Type**

Some posts ago when we were working with the *`BST`* we had to create a new type called *`Tree`*. Let’s see how we did this:
```haskell
data Tree a = Empty | Node a (Tree a) (Tree a)
```
Similar *`Boolean`* data type we have a type called *`Tree`*, and similar *`Boolean`* value constructors our type has two called *`Empty`* and *`Node`*.  
We can run that in *`GHCI`*:
```haskell
data Tree a = Empty | Node a (Tree a) (Tree a)

> :t Empty
Empty :: Tree a
> :t Node
Node :: a -> Tree a -> Tree a -> Tree a

> let empty = Empty
> :t empty
empty :: Tree a

> let node = Node 3 Empty Empty
> :t node
node :: Num a => Tree a
```

We see that we create a new data type and we are using this.

<br />

In the next posts we'll still working with our own data types.
