---
layout: post
title: Haskell's Marathon - Days Twenty Seven to Twenty Eight
published: true
lang: en
translation: true
---

Hey folks!

Last post we saw how to build a *`Binary Tree Search (BST)`* from a list. Today we will talk about *`insert`* function which can add a node in a *`BST`*.  

<br />

**BST Recap**

We already know how to build a *`BST`* from a list. We have a *`build`* function and an auxiliary function to help us. The auxiliary function is used to get an accumulator which is our tree.

<!--more-->

```haskell
build' :: (Ord a, Eq a) => [a] -> Tree a -> Tree a
build' [] tree = tree
build' (x:xs) Empty = build' xs (Node x Empty Empty)
build' (x:xs) (Node a left right)
  | a >= x = build' xs (Node a (build' [x] left) right)
  | otherwise = build' xs (Node a left (build' [x] right))

build :: (Ord a, Eq a) => [a] -> Tree a
build xs = build' xs Empty

build [8,6,9,4,7,11,10,12,8,6,2,3,1]
Node 8 (Node 6 (Node 4 (Node 2 (Node 1 Empty Empty) (Node 3 Empty Empty)) (Node 6 Empty Empty)) (Node 7 Empty (Node 8 Empty Empty))) (Node 9 Empty (Node 11 (Node 10 Empty Empty) (Node 12 Empty Empty)))
```

I guess we can improve these functions.

<br />

**Create a Single Node**

First of all let’s create a helper function called *`singleNode`* which receives a value and creates a node just with one value and the left and right sides are empty.
```haskell
singleNode :: (Ord a) => a -> Tree a
singleNode x = Node x Empty Empty
```
Too simple that it is self explanatory.

<br />

**Insert a Node in Tree**

Now we can create a function to insert a new value in a *`BST`*. This function receives the tree which we want add a value and the value. The output of *`insert`* functions is the tree received with a new element.
```haskell
insert :: (Ord a) => Tree a -> a -> Tree a
insert Empty x = singleNode x
insert (Node a left right) x
  | a >= x = Node a (insert left x) right
  | otherwise = Node a left (insert right x)
```

Here we are using the function *`singleNode`* which we created above just to make our code cleaner.  
The *`insert`* function is really simple just looks for the correct place to add the new value. To do this the function navigates in the left and right sides of the tree.

<br />

**Improving the build function**

Before we had a *`build`* function as:
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
If we take a look in these functions we can see that they have some similarities with *`insert`* function. So let’s try improve the *`build`* function using the *`insert`* function.
```haskell
build' :: (Ord a, Eq a) => [a] -> Tree a -> Tree a
build' [] tree = tree
build' (x:xs) tree = build' xs $ insert tree x

build :: (Ord a, Eq a) => [a] -> Tree a
build xs = build' xs Empty
```
For me it’s much better. And for you?
We had a *`build’`* function with 5 lines and now we have just 2. Now the *`build’`* function is cleaner and more meaningful.

<br />

**More two options**

Beyond that we can improve more our *`build`* function.  
First we can move the *`build’`* function inside the *`build`* function and use it as a variable internally.
```haskell
build :: (Ord a) => [a] -> Tree a
build [] = Empty
build xs = build' xs Empty
  where
    build' (y:ys) Empty = build' ys $ insert Empty y
    build' (y:ys) tree = build' ys $ insert tree y
```
We can say that we had some improvement because we don’t need an auxiliary function. But looks like that we didn’t have a huge improvement.

We can improve a little bit more. Let’s try?
```haskell
build :: (Ord a) => [a] -> Tree a -> Tree a
build [] tree = tree
build (x:xs) tree = build xs $ insert tree x
```
Now I think we have a good improvement. We remove the auxiliary function and our *`build`* function has just 2 lines and it is really readable.  
What do you think?

<br />

Split a function in small functions is a good practice in Functional Programming. The idea is have small functions with just one responsibility and functions use other functions to achieve their goal. It was what we did with *`build`*. We created a new *`insert`* function which has the only one responsibility to add a new element in a tree. And we used the *`insert`* function in our *`build`* function. This made our *`build`* function simpler and gave us the opportunity to improve it. Because simple and readable code is easier to refactor and we have more confidence to do this.
