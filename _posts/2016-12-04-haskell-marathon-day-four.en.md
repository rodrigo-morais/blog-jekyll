---
layout: post
title: Haskell's Marathon - Day Four
published: true
lang: en
translation: true
---

Hey folks!


Today we will talk a little bit more about lists, but we will take a look in tuples too.

<br />

**List Comprehension**

In the days two and three we saw how create and use lists, today we will talk about another way to use lists called list comprehension.
List comprehensions are the way to transform, filter and combine lists. It is similar to the mathematical concept of set comprehensions, but we are won’t pay attention to it.
Let’s start saying that we want generate a list of values from 1 to 10 and multiply per 2. With list comprehension we can do in this way:
```haskell
[ x*2 | x <- [1..10]]
[2,4,6,8,10,12,14,16,18,20]
```

Pretty easy. Let’s do it a little bit more complex and say that we just want values bigger than 10:
```haskell
[ x*2 | x <- [1..10], x*2 > 10]
[12,14,16,18,20]
```

Another thing beyond transformation and filter of list which we can do with list comprehensions is combination. Let’s combine  three lists?
```haskell
[x+y+z | x <- [1,2,3], y <- [101,102,103], z <- [1001,1002,1003]]
[1103,1104,1105,1104,1105,1106,1105,1106,1107,1104,1105,1106,1105,1106,1107,1106,1107,1108,1105,1106,1107,1106,1107,1108,1107,1108,1109]
```

Now let’s try the list comprehension with a list of list and just get the odd numbers from it:
```haskell
let a = [1,2,3,4,5]
let b = [7,8,9,2,3,4,5]
let c = [11,12,13,14,15,16,17,18]
[ [ x | x <- xs, odd x ] | xs <- [a,b,c] ]
[[1,3,5],[7,9,3,5],[11,13,15,17]]
```

The list comprehension is really powerful feature from *`Haskell`*, and we will work more with it today.

<br />

**Tuples**

Tuples are used in *`Haskell`* to store heterogeneous types. There are some similarities between lists and tuples, but tuples beyond be heterogeneous they have a fixed size too.
```haskell
(1,2)
(1,2)
(1,2,”hello”)
(1,2,”hello”)
(1,2,”hello”, True)
(1,2,”hello”, True)
```

Tuples have a fixed size then we should use they just when we know how much elements we will need.
When tuples have two elements we can use the functions *`fst`* and *`snd`*.
```haskell
fst (2,5)
2
snd (2,5)
5
```

We can use the list comprehension which we saw before combined with tuples and get all combinations from the lists. Let’s try it:
```haskell
[(x,y,z) | x <- [1,2,3], y <- [101,102,103], z <- [1001,1002,1003]]
[(1,101,1001),(1,101,1002),(1,101,1003),(1,102,1001),(1,102,1002),(1,102,1003),(1,103,1001),(1,103,1002),(1,103,1003),(2,101,1001),(2,101,1002),(2,101,1003),(2,102,1001),(2,102,1002),(2,102,1003),(2,103,1001),(2,103,1002),(2,103,1003),(3,101,1001),(3,101,1002),(3,101,1003),(3,102,1001),(3,102,1002),(3,102,1003),(3,103,1001),(3,103,1002),(3,103,1003)]
```

Here each tuple is a combination.

<br />

Tomorrow we will start dive in *`Haskell’s`* types.
