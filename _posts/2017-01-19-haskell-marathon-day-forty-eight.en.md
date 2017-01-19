---
layout: post
title: Haskell’s marathon - Day Forty Eight
published: true
lang: en
translation: false
---

Hey folks!

Last posts we learned how to create our own data type. Today we will see how to export our data type in a *`module`*. 

<br />

**Module**

Some posts ago we saw how create a *`module`* and we created one to our *`BST`*. Our *`module`* exports some functions to work with a *`BST`*:
<!--more-->
```haskell
module BST
( build
, build2
, build3
, insert
, find
, findSub
, contains
, size
, height
, delete
) where
```
But our *`BST`* has a data type and we can export it.
```haskell
module BST
( Tree(..)
, build
, build2
, build3
, insert
, find
, findSub
, contains
, size
, height
, delete
) where
```
If see the first element exported in the module is our data type as *`Tree(..)`*. Here we are saying that we are exporting all value constructors from our data type and now we can use them:
```haskell
> :t Empty
Empty :: Tree a

> :t Node
Node :: Ord a => a -> Tree a -> Tree a -> Tree a
```
Cool. Is possible export just some data types as:
```haskell
module BST
( Tree(Empty)
, build
, build2
, build3
, insert
, find
, findSub
, contains
, size
, height
, delete
) where

> :t Empty
Empty :: Tree a

> :t Node
<interactive>:1:1: Not in scope: data constructor ‘Node’
```
Is possible just import only the data type without value constructors:
```haskell
module BST
( Tree
, build
, build2
, build3
, insert
, find
, findSub
, contains
, size
, height
, delete
) where

> :t Empty
<interactive>:1:1: Not in scope: data constructor ‘Empty’

> :t Node
<interactive>:1:1: Not in scope: data constructor ‘Node’
```
<br />

Now we already know how export functions and data types in our *`modules`*.
