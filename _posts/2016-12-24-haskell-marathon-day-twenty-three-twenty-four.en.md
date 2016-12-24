---
layout: post
title: Haskell's Marathon - Days Twenty Three to Twenty Four
published: true
lang: en
translation: true
---

Hey folks!

These last days I’m working in some exercises and I want invite you to create a *`Binary Search Tree (BST)`* with me.  
The *`BST`* is a data structure which has the data ordered making easier to search for a data inside it. The *`BST`* follows a rule where the smaller or equal values compared with the root should be on the left side of the root and the bigger values on the right. Because of that the values in a *`BST`* should be comparable as Int, Char and etc are.

<!--more-->

Let’s say that we have a list as: [5,3,6,3,2,7,1,8,9]  
This list will create a tree like that:

<image src="{{site.url}}/images/bst_1.png" />

Can you see that the numbers in the list just grew to left or right in the tree? In this case we have a tree with left and right side, and a bunch of sub-trees with left or right side just.

How we created this tree from the list?  
First we get the first element from the list which was the number 5. After that we get the second value which was 3 and compared with 5. The number 3 is smaller than number 5 and because of that we put on the left side of the root which was the number 5. Now we have a tree which the root is the number 5, the left side has a leaf which is the number 3 and the right side is empty.  
Following our list the next value is the number 6 which is bigger than the root 5 and should be on the right side. Now we have a tree with two leaves on left and right side.  
Next value is 3 which is smaller than the root 5 and should be on the left. So we have to compare with the next value which is 3 too and because of that the value should be on the left. Now we have a sub-tree which has the root 3, the left side with the number 3 and the right side empty.  
This process happened with all numbers in our list and finished creating our tree above.


Now let’s see how to create a *`BST`* in *`Haskell`*:
```haskell
data Tree a = Empty | Node a (Tree a) (Tree a)
  deriving Show

:t Node
Node :: a -> Tree a -> Tree a -> Tree a

:t Empty
Empty :: Tree a
```
Now we have a type *`Tree a`* with two differents options which are *`Empty`* and *`Node a (Tree a) (Tree a)`*. The *`Tree`*, *`Empty`* and *`Node`* are not types or values from *`Haskell`* but we are creating them to our program. In the future we will talk more about that, but for a while we can think in them as types as Int, Char and etc.  
Another point is the *`deriving Show`* which we associated with our type. It is to be possible print our tree.

Now let’s write a really simple function which say if a *`BST`* is empty or not. If the *`BST`* has the value *`Empty`* than it is empty otherwise not.
```haskell
empty :: Tree a -> Bool
empty Empty = True
empty _ = False

let emptyTree = Empty
empty emptyTree
True

let tree = Node 3 Empty Empty
empty tree
False
```
Pretty simple function which say if our *`BST`* is empty or not.

