---
layout: post
title: Haskell's Marathon - Days Thirty Four to Fourty
published: true
lang: en
translation: true
---

Hey folks!

Last post we saw some functions to calculate the size and height of our *`Binary Search Tree (BST)`*.  
Today is the last post about the exercises with *`BST`* and we will create the function to remove nodes from.

<br />

**BST Recap**

Let's just recap how were the functions *`size`* and *`height`* which we worked in the last post.

First the function *`size`* to work with a *`BST`* which means get a number of elements that exist in a *`BST`*.
 *`BST`*.
```haskell
size :: (Ord a) => Tree a -> Int
size Empty = 0
size (Node _ left right) = 1 + (size left) + (size right)

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

<!--more-->

Pretty straightforward function to count the number of nodes.

Now let’s see the function *`height`* which gives us the height of a *`BST`*.
```haskell
height :: (Ord a) => Tree a -> Int
height Empty = 0
height (Node _ left right) = (+) 1 $ max (height left) (height right)

> newTree
Node 6 (Node 4 (Node 2 (Node 1 Empty Empty) (Node 3 Empty Empty)) (Node 6 Empty Empty)) (Node 7 Empty (Node 8 Empty Empty))

> height newTree
4
```
The function look simple, but it is not easy to understand the computation under the hood. If you have some doubt I suggest you take a look in the previous [post](https://rodrigo-morais.github.io/haskell-marathon-day-thirty-two-thirty-three/).

<br />

**Delete node in a *`BST`***

We already have functions to create a *`BST`* from a list, add new node, find a node and evaluate if a value exist or not in our tree. Now we have to do the last function which is to remove a node from our *`BST`*.  
Let’s say that we have this *`BST`*:  

<image src="{{site.url}}/images/bst_6.png" />

We can start trying to remove the node with number 10. This is pretty easy, because this node doesn’t have other nodes on left or right. We just have to remove it.  
Let’s see how is the *`delete`* function:
```haskell
empty :: Tree a -> Bool
empty Empty = True
empty _ = False

findSmallest :: (Ord a) => Tree a -> a
findSmallest Empty = error "Empty list"
findSmallest (Node a left _)
  | empty left = a
  | otherwise = findSmallest left

delete :: (Ord a) => Tree a -> a -> Tree a
delete Empty _ = Empty
delete (Node a left right) x
  | a == x && empty right = left
  | a == x && empty left = right
  | a == x = Node smaller left newRight
  | a >= x = Node a (delete left x) right
  | otherwise = Node a left (delete right x)
  where smaller = findSmallest right
        newRight = delete right smaller
```
The *`delete`* function uses two helper functions to remove a node which are *`empty`* and *`findSmallest`*. The function *`delete`* works recursively. Let’s see how is the process to remove the value 10:  
  * First value is 8 and it is compared with value 10 which we want remove. The number 8 is smaller than 10 and the value 10 must be on the right side of the tree.
  * Move to next element on right which is 12. The number 12 is bigger than 10 and the evaluation should continue on the left side of the node 12.
  * Move to next element on left which 11. The number 11 is bigger than 10 and the evaluation should continue on the left side of the node 11.
  * Move to next element on left which 10. The number 10 is the number that we are looking for. The first evaluation in this case in our function is if the right side of the node is empty. And it is. So we return the left side which in this case is empty too.  


And we have the same tree without the node with value 10.  

<image src="{{site.url}}/images/bst_7.png" />

Now let’s try to remove the value 12 from the original tree. But what we will do with the left and right sides of this node if they are not empty? The result will be:

<image src="{{site.url}}/images/bst_8.png" />

The function *`delete`* remove the node with value 12 and move the smallest node on right, which in this case is the node with value 18, to the removed node place. Let see how is it works:  
  * First value is 8 and it is compared with value 10 which we want remove. The number 8 is smaller than 10 and the value 10 must be on the right side of the tree.
  * Move to next element on right which is 12. The number 12 is what we are looking for. So we have to looking for the smallest value in the right side of this sub-tree.
  * Using the helper function *`findSmallest`* we dicover that the smallest value on right is 18.
  * We recreate the tree putting the node with value 18 where the node with value 12 is.

Both the process and the function are not simple to understand, but it is a good exercise to training *`Haskell`*

<br />

The source code to our *`BST`* is in [this repository](https://github.com/rodrigo-morais/haskell-exercises/blob/master/binary-tree.hs).
