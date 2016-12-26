---
layout: post
title: Haskell's Marathon - Days Twenty Five to Twenty Six
published: true
lang: en
translation: true
---

Hey folks!

Last post we talked about *`Binary Tree Search (BST)`* and we saw how to create a type to work with and how to write a simple function too.  
Today we will see how build a *`BST`* from a list.

<br />

**BST Recap**

We already know that we have to create a new type to work with a *`BST`*:
```haskell
data (Ord a, Eq a) => Tree a = Empty | Node a (Tree a) (Tree a)
  deriving Show
```

<!--more-->

In our type the *`BST`* can have two differents values which are *`Empty`* or *`Node a (Tree a) (Tree a)`*. The *`Empty`* is just a empty tree. And the *`Node a (Tree a) (Tree a)`* is a branch from a tree which has a new branch to left and another to right.

Beyond the *`BST`* data structure we wrote a simple function to see if a tree is empty or not.
```haskell
empty :: Tree a -> Bool
empty Empty = True
empty _ = False
```

<br />

**Build a Tree**

In this moment we can create a *`BST`* manually like this:
```haskell
let x = Node 8 (Node 6 (Node 4 (Node 2 (Node 1 Empty Empty) (Node 3 Empty Empty)) (Node 5 Empty Empty)) (Node 7 Empty Empty)) (Node 10 (Node 9 Empty Empty) (Node 11 Empty Empty))

x
Node 8 (Node 6 (Node 4 (Node 2 (Node 1 Empty Empty) (Node 3 Empty Empty)) (Node 5 Empty Empty)) (Node 7 Empty Empty)) (Node 10 (Node 9 Empty Empty) (Node 11 Empty Empty))

:t x
x :: (Num a, Ord a) => Tree a
```
But create *`BST`*  manually is pretty boring and would be great if we could convert a list in a tree.  
Let’s say that we have this list: [8,6,9,4,7,11,10,12,8,6,2,3,1]  
How is the *`BST`* built with this list?

<image src="{{site.url}}/images/bst_2.png" />

This is a much more complex *`BST`* than the *`BST`* which we saw in the last post. Let’s see how to build that *`BST`* in *`Haskell`*:
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

Here the function *`build`* receives a list and build a *`BST`*, but this function just call the auxiliary function *`build’`*.  
The function *`build’`* will do all dirty work. It receives a list, a tree and return a tree. The function *`build`* call the function *`build’`* with a list which was received and an empty tree.  
With this data the function *`build’`* will call itself recursively. Let’s think in our list above which is not empty.  
First the tree is empty, then the first element of our list which is 8 is the root of our tree. After the value 6 which is smaller than the root and it is added on the left. Next value is 9 which is bigger than the root and because of that we add on the right.  
The other values will follow the same idea.

Let’s see the function working:
```haskell
build [8,6,9,4,7,11,10,12,8,6,2,3,1]
Node 8 (Node 6 (Node 4 (Node 2 (Node 1 Empty Empty) (Node 3 Empty Empty)) (Node 6 Empty Empty)) (Node 7 Empty (Node 8 Empty Empty))) (Node 9 Empty (Node 11 (Node 10 Empty Empty) (Node 12 Empty Empty)))
```

It is our list as a *`BST`*.

<br />

Is possible to make this *`build`* function better and smaller. In the next posts we will work in some helper functions which will help to rewrite the *`build`* function.
