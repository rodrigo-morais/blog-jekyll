---
layout: post
title: Haskell's Marathon - Days Twenty Nine to Thirty One
published: true
lang: en
translation: true
---

Hey folks!

Last post we improved our *`build`* function and saw some options using the *`insert`* function which we created to add nodes in our *`BST`*.  
Now let’s see some functions to find an element in the tree or confirm if the tree contains or not an element.

<br />

**BST Recap**

First let’s do a quick recap how we arrived til here.

We started creating a type to our *`BST`*.
```haskell
data (Ord a, Eq a) => Tree a = Empty | Node a (Tree a) (Tree a)
  deriving Show
```

<!--more-->

In the second post we saw how to build a *`BST`* from a list.
```haskell
build' :: (Ord a, Eq a) => [a] -> Tree a -> Tree a
build' [] tree = tree
build' (x:xs) Empty = build' xs (Node x Empty Empty)
build' (x:xs) (Node a left right)
  | a >= x = build' xs (Node a (build' [x] left) right)
  | otherwise = build' xs (Node a left (build' [x] right))

build :: (Ord a, Eq a) => [a] -> Tree a
build xs = build' xs Empty
```

In the last post we created the *`insert`* function:
```haskell
singleNode :: (Ord a) => a -> Tree a
singleNode x = Node x Empty Empty


insert :: (Ord a) => Tree a -> a -> Tree a
insert Empty x = singleNode x
insert (Node a left right) x
  | a >= x = Node a (insert left x) right
  | otherwise = Node a left (insert right x)
```
Using our *`insert*` function we saw some options of improvement to *`build`* function:
```haskell
build' :: (Ord a, Eq a) => [a] -> Tree a -> Tree a
build' [] tree = tree
build' (x:xs) tree = build' xs $ insert tree x

build :: (Ord a, Eq a) => [a] -> Tree a
build xs = build' xs Empty


build2 :: (Ord a) => [a] -> Tree a
build2 [] = Empty
build2 xs = build2' xs Empty
  where
    build2' (y:ys) Empty = build2' ys $ insert Empty y
    build2' (y:ys) tree = build2' ys $ insert tree y


build3 :: (Ord a) => [a] -> Tree a -> Tree a
build3 [] tree = tree
build3 (x:xs) tree = build3 xs $ insert tree x
```

<br />

**Find a Node in the Tree**

Now let’s looking for a node inside a *`BST`* and let’s return it as a tree.
```haskell
find :: (Ord a) => Tree a -> a -> Tree a
find Empty _ = Empty
find (Node a left right) x
  | a == x = Node a left right
  | a >= x = find left x
  | otherwise = find right x
```
This return a node with its left and right sides according the value received.  
Let’s say that we have this tree:

<image src="{{site.url}}/images/bst_2.png" />

If we call the *`find`* function with value 6 we will receive this *`BST`* as result:

<image src="{{site.url}}/images/bst_3.png" />

**Find a Node in the Tree which is Not Root**

Cool, but our *`BST`* has two six and if after we call the *`find`* function over the original tree, received a new tree with a 6 as root and tried to get the second 6. It won’t get the second 6.  
So we have a new function to get the second 6:
```haskell
findSub :: (Ord a) => Tree a -> a -> Tree a
findSub Empty _ = Empty
findSub (Node a left right) x
  | a >= x = find left x
  | otherwise = find right x
```
We could do that without a function, but it makes our life easier.

<br />

**Verify if Tree contains an Element**

Our last helper function is to verify if our *`BST`* contains or not a value:
```haskell
contains :: (Ord a) => a -> Tree a -> Bool
contains _ Empty = False
contains x (Node a left right)
  | a > x = contains x left
  | a < x = contains x right
  | otherwise = True
```
Thinking in the previous *`BST`* if we call *`contains`* function with value 7 it will return *`True`* and if we call with 5 will return *`False`*.
