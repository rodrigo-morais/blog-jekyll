---
layout: post
title: Haskell's Marathon - Day One
published: true
lang: en
translation: true
---

Today is my first day in *`Haskell’s`* marathon and I’d like to share with you what are my learning and understanding.

<br />

**Set up**

Let’s start how set up your computer to use *`Haskell`*. You have to install the *`Haskell`* compiler called *`GHC`*. The steps are in this [link](https://www.haskell.org/platform/).
My tip here is don’t install the *`Haskell`* compiler in your machine, instead that use a *`Docker`* image with *`Haskell`* to work with. If you don’t have *`Docker`* in your computer you can see how install it here: [https://www.docker.com/products/overview](https://www.docker.com/products/overview). After install *`Docker`* you just have to start it and run this command: **docker run -ti --rm -v $(pwd):/code haskell:7.10 bash**. Now you have a virtual machine running the *`Haskell`* compiler to you. To start the *`GHC's interpreter`* you have to run the command: **ghci**.

<!--more-->

<br />

**Immutability**

*`Haskell`*, as a pure functional language, works with immutability. It means that you don’t have variables and when you set a value to a “container” / “repository” is impossible change it. *`Haskell`* doesn’t have side effects and it gives us the reliability that always we call a function with one value we will receive the same return. This characteristic increases the *`Haskell`* testability and we don’t have to looking for in a bunch of line of code where happened the value change and why it is affecting my function.

<br />

**Lazy**

*`Haskell`* is *`lazy`*. It means that *`Haskell`* just does the computation which is necessary and wait till the last moment to execute some functions to return the result.
For example, let’s say that we have a list with 1000 numbers and we want to convert this list in a list of modules and get the first value, to do it *`Haskell`* will go through the list till find the first value and will stop.
```haskell
let xs = [1..999999]
xs
map (\x -> x `mod` 2) xs
head (map (\x -> x `mod` 2) xs)
```
With this example you can see how the *`Haskell’s`* laziness is powerful. When we run the lines 2 and 3 we have a delay till receive the all result on the other hand when we run the line 4 we receive the result almost automatically. It happens because *`Haskell`* stop the process as soon as find out the result.

<br />

**Static Type**

*`Haskell`* is statically typed, but different the languages as *`Java`* or *`C#`* we don’t have to assign a type for everything. *`Haskell`* infers the types to values and functions and use the compiler to evaluate errors. Therefore *`Haskell`* isn't considered a verbose language.

<br />

**Arithmethic**

To do arithmetic in *`Haskell`* is similar than other languages. It follows the precedents universal from math.

<br />

**Boolean**

Booleans in *`Haskell`* are similar with other languages too. We have the values *`True`* and *`False`* the operators *`&&`* (and), *`||`* (or) and *`not`* (negate). To test two values we have the operators *`==`* (equal) and *`/=`* (not equal). Test them in the *`GHCI`*.

<br />

**Functions**

Everything in *`Haskell`* are functions or at least almost everything. We could not realized but *`+`* and *`-`* are functions. These kind of functions are called *`infix`* because they are called between the operands as *`5 + 6`*. Most functions are *`prefix`*, where they are called before the operands as *`succ 9`*. *`Prefix`* functions can be called as *`infix`* functions, to do this we have to surround them in brackticks (\`) as *9 \`div\` 3*. The opposite is possible too, and in this case we have to surrond the function with parentheses (()).  
To create a function we have to give to it a name and the parameters. When we create a function in *`GHCI`* is necessary to use *`let`*, but if we create a function in a file which will be compiled we mustn't use *`let`*.
Let’s create some functions?
```haskell
Let mult2 x = x * 2
mult2 3
6
mult2 4
8
let add x y = x + y
add 2 3
5
add 3 3
6
```

<br />

These was my first steps with *`Haskell`*.
