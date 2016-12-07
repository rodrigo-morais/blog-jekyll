---
layout: post
title: Haskell's Marathon - Day Seven
published: true
lang: en
translation: true
---

Hey folks!


Today the study about *`Haskell`* was a little bit different. Instead of to follow the book I went in a meetup. It was my first meetup here in Berlin and was pretty cool and different.  
This meetup happens every Wednesday and each week with different goals. One week is a meetup with lectures and etc, and another week is to beginners learn the language.  
Today the meetup was to beginners. The group is following the book called [“Haskell Programming”](http://haskellbook.com/) and today they covered the eighth chapter which is about *`foldr`* and *`foldl`*.

<!--more-->

The meetup started with a review about the chapter seven which was about Lists and functions as *`map`*, *`filter`* and *`zip`*. The cool part here was that we discuss how implement these functions manually. It was interessant because the participants could share ideas and experiences and we were building the solutions together. And beyond that we become more aware about this functions and after that is easier use them.


After that we talk about the functions *`foldr`* and *`foldl`* which are useful to work with lists. They work as *`reduce`* works in other languages.
```haskell
foldr (+) 0 [1..10]
55
foldl (+) 0 [1..10]
55
```
The difference is that one start from left and another from right. We will talk about this functions and *`map`*, *`filter`*, *`zip`* and etc soon.

<br />

If you come to Berlin or you are in Berlin I really recommend this [meetup](https://www.meetup.com/berlinhug/). Really smart and helpful people with different backgrounds and levels about *`Haskell`*.
