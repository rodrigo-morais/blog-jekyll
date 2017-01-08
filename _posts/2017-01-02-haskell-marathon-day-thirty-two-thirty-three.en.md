---
layout: post
title: Haskell's Marathon - Days Thirty Two to Thirty Three
published: true
lang: en
translation: true
---

Hey folks!

Last post we saw some functions to find an element in the tree or confirm if the tree contains or not an element.
Today we will learn how to calculate the size and height of our *`BST`*.

<br />

**BST Recap**

First let’s do a quick recap about find elements and confirm if an element exists or not in our *`BST`*.

First how we find an element in our tree.
```haskell
find :: (Ord a) => Tree a -> a -> Tree a
find Empty _ = Empty
find (Node a left right) x
  | a == x = Node a left right
  | a >= x = find left x
  | otherwise = find right x
```

<!--more-->

And when we have duplicated elements in tree, how we get the second one?
```haskell
findSub :: (Ord a) => Tree a -> a -> Tree a
findSub Empty _ = Empty
findSub (Node a left right) x
  | a >= x = find left x
  | otherwise = find right x
```

Let’s confirm if the element exist or not in the tree:
```haskell
contains :: (Ord a) => a -> Tree a -> Bool
contains _ Empty = False
contains x (Node a left right)
  | a > x = contains x left
  | a < x = contains x right
  | otherwise = True
```

<br />

**Calculating the *`BST`* size**

One important feature when we are working with *`BST`* is get the size of a tree.  
The size means the number of element which a *`BST`* contains. So let’s create a function for that:
```haskell
size :: (Ord a) => Tree a -> Int
size Empty = 0
size (Node _ left right) = 1 + (size left) + (size right)
```
The function is really simple. We receive a tree and return the number of element as an Int.  
If the tree is *`Empty`* should the function *`size`* returns the value 0. Otherwise if the tree is not *`Empty`* the *`size`* function will sum 1 and call itself to sub-trees on left and right.

This function works recursively calling itself till find an *`Empty`* node.  
Let’s see how it works:
```haskell
> let tree = build [8,6,9,4,7,11,10,12,8,6,2,3,1]
> tree
Node 8 (Node 6 (Node 4 (Node 2 (Node 1 Empty Empty) (Node 3 Empty Empty)) (Node 6 Empty Empty)) (Node 7 Empty (Node 8 Empty Empty))) (Node 9 Empty (Node 11 (Node 10 Empty Empty) (Node 12 Empty Empty)))

> size tree
13

> let newTree = find tree 6
> newTree
Node 6 (Node 4 (Node 2 (Node 1 Empty Empty) (Node 3 Empty Empty)) (Node 6 Empty Empty)) (Node 7 Empty (Node 8 Empty Empty))

> size newTree
8
```

<br />

**How tall are you?**

Another really useful function when we are working with *`BST`* is the function *`height`*. This function gives us the height of the tree and can be used to balance a tree. How we can see a *`BST`* is not a balanced tree.  
For example if we have a list in sequence as: [3,4,5,6,7]  
We have this *`BST`*:

<image src="{{site.url}}/images/bst_4.png" />

We can see that the tree is unbalanced to right. We have some algorithmus to balance a tree and they use the *`height`* function for that.  
For a while we will pay attention just in the *`height`* function.
```haskell
height :: (Ord a) => Tree a -> Int
height Empty = 0
height (Node _ left right) = (+) 1 $ max (height left) (height right)
```

It is a small function, but not so simple to understand.  
First if the tree is *`Empty`* the height is 0.  
If the tree is not *`Empty`* we should sum 1 for the root and get the maximum height between the left and right side. The *`height`* function will dive until find an *`Empty`* node and start to count the height from bottom to top. It works recursively.

Let’s say we have this *`BST`*:

<image src="{{site.url}}/images/bst_3.png" />

Cool. If we call the function:
```haskell
> newTree
Node 6 (Node 4 (Node 2 (Node 1 Empty Empty) (Node 3 Empty Empty)) (Node 6 Empty Empty)) (Node 7 Empty (Node 8 Empty Empty))

> height newTree
4
```

How is it work?  
First we get the height to left side. Then we start with the first tree from bottom to top. 

<image src="{{site.url}}/images/bst_5.png" />

In this first tree we have a node which is the root with value 2 and with a node on left and one on right. The left and right nodes don’t have nodes to left or right or they have *`Empty`* nodes. The *`Empty`* nodes return the height 0.  
Cool, so the node with value 1 is a root of a sub-tree which the left and right sides are *`Empty`*. We have the function which treats it as:  
(+) 1 $ max (height left) (height right) => (+) 1 max 0 0 => (+) 1 0 => 1  
The same happens with the right side of tree where the sub-tree has a root as 3.  
Now we can go to the root of our three which is 2. Let’s see how it works:  
(+) 1 $ max (height left) (height right) => (+) 1 $ max 1 1 => (+) 1 1 => 2  
Here we get the height of our sub-trees, we compare to get the maximum and after we sum 1 which came from the root always.  

This process will be repeated in whole tree till achive the root.  

Let’s finish it. Now we know the height of left side of sub-tree where the root is 4. The right side just have one node with the left and right sides *`Empty`* and because of that the height is 1. With that we have this function:  
(+) 1 $ max (height left) (height right) => (+) 1 $ max 2 1 => (+) 1 2 => 3  
Now we know that the left side of tree has the height as 3.  
The right side has a sub-tree where the left side is *`Empty`* and the right side just have a single node with height 1 making the right's sub-tree height equal 2.    
With this data we can sum the height of our tree:  
(+) 1 $ max (height left) (height right) => (+) 1 $ max 3 2 => (+) 1 3 => 4  

And we have the same result of our function.
