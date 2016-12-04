---
layout: post
title: Haskell's Marathon - Day Three
published: true
lang: en
translation: true
---

Hey folks!


Let’s continue taking a look in lists?  
Yesterday we took a look in how concatenate and get element from a list. Today we will see other feature which *`Haskell`* provides to his lists.

<br />

**Nested lists**

This is pretty simple and obvious. Lists in *`Haskell`* can contain numbers, strings, booleans and other lists.
Let’s take a look how to do this:
```haskell
[[1,2,3],[4,5,6]]
[[1,2,3],[4,5,6]]
[['h','e','l','l','o'],['w','o','r','l','d']]
["hello","world"]
[[1,2,3],['h','i']]
<interactive>:43:3:
    No instance for (Num Char) arising from the literal ‘1’
    In the expression: 1
    In the expression: [1, 2, 3]
    In the expression: [[1, 2, 3], ['h', 'i']]
```
In the case of nested lists the rule about types still mandatory. As we can see in the last example we can’t combine two lists with different types.

<br />

**Comparing Lists**

*`Haskell`* allowed us to compare lists if their items are comparable. When we use *`<`*, *`<=`*, *`==`*, *`/=`*, *`>`* or *`>=`* to compare two lists, they are compared in lexicographical order. It means that the first two heads are compared, and if they are equal, the second elements are compared and so on.
Let’s see how comparing works:
```haskell
let listA = [1,2,3]
let listB = [1,2,3]
let listC = [1,3,4]
listA == listB
True
listA /= listB
False
listA == listC
False
listA >= listC
False
listA <= listC
True
```
<br />

**Other operations**

*`Haskell`* has more operations to work with lists. Let’s take a quick look in them:
```haskell
head [1,2,3,4,5] -- gets the first element from the list
1
tail [1,2,3,4,5] -- gets the list without the first element
[2,3,4,5]
head [] -- returns an error when list is empty
*** Exception: Prelude.head: empty list
tail [] -- returns an error when list is empty
*** Exception: Prelude.tail: empty list
tail [1] -- returns an empty list when the list has only one element
[]
init [1,2,3,4] -- the opposite of tail. Returns all list less the last element
[1,2,3]
init [1] -- returns an empty list if it has just one element
[]
last [1,2,3] -- returns the last element of the list
3
length [1,2,3,4,5] -- returns the size of the list
5
length []
0
null [1,2] -- returns if the list is null or not
False
null []
True
reverse [5,4,3,2,1] -- reverses the list
[1,2,3,4,5]
reverse [1,2,3,4,5]
[5,4,3,2,1]
take 3 [3,4,2,6,3,1,8] -- takes the number of elements asked from the list
[3,4,2]
take 30 [3,4,2,6,3,1,8]
[3,4,2,6,3,1,8]
drop 3 [3,4,2,6,3,1,8] -- removes the number of elements from the list
[6,3,1,8]
drop 30 [3,4,2,6,3,1,8]
[]
maximum [2,9,6,4,3,7,8] -- gets the maximum element in the list
9
minimum [2,9,6,4,3,7,8] -- gets the minimum element in the list
2
sum [2,9,6,4,3,7,8] -- sums the elements from the list
39
product [2,9,6,4,3,7,8] -- multiplies the elements from the list
72576
4 `elem` [2,9,6,4,3,7,8] -- verifies if the element is contained in the list
True
1 `elem` [2,9,6,4,3,7,8]
False
```
<br />

**Range of list**

Sometimes we have to create huge lists and *`Haskell`* has one way to help us with it. We have to use a range in a list. This is pretty simple, but really powerful.
```haskell
[1..20]
[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]
['A'..'s']
"ABCDEFGHIJKLMNOPQRSTUVWXYZ[\\]^_`abcdefghijklmnopqrs"
[3,6..12]
[3,6,9,12]
[1..] -- infinite numbers
take 5 [1..] -- takes the first five number from an infinite list of numbers
[1,2,3,4,5]
```
<br />

Today we learnt some new operations with lists.
