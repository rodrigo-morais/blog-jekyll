---
layout: post
title: Haskell's Marathon - Day Nine
published: true
lang: en
translation: true
---

Hey folks!


Yesterday we talked about *`Pattern Matching`* and today we will start with a special case of *`Pattern Matching`*. If we need get the whole list during a *`Pattern Matching`* we can use something called *`as-pattern`*. I don’t think this special case not much useful, but I’ll show you one example:
<!--more-->
```haskell
firstLetter :: String -> String
firstLetter all@(x:xs) = "The first letter of " ++ all ++ " is " ++ [x]


firstLetter "Haskell"
"The first letter of Haskell is H"
```


Now we will talk about something important. *`Guards`* are another way to do *`Pattern Matching`* where we can compare values. It is more similar with *`IF/ELSE`* than *`Pattern Matching`* is. When we receive a value we can valid if some property from it is true or false what we can’t do it with *`Pattern Matching`*, but we can with *`Guards`*. Let’s see an example:
```haskell
bmiStatus :: Double -> Double -> String
bmiStatus weight height
  | weight / height ^ 2 <= 18.5 = "You are underweight!"
  | weight / height ^ 2 <= 25 = "You are with ideal weight!"
  | weight / height ^ 2 <= 30 = "You are overweight!"
  | otherwise = "You are obese!"


bmiStatus 85 1.81
"You are overweight!"


bmiStatus 80 1.81
"You are with ideal weight!"


bmiStatus 60 1.81
"You are underweight!"


bmiStatus 100 1.81
"You are obese!"


```
The *`Guards`* looks like *`Pattern Matching`*, but we can compare values and do actions if the comparison is true or false. Instead of *`Pattern Matching`* which evaluates the pattern.


But in this function where we are calculating if some person is fit or not comparing his/her weight and height we are repeating three times the same calculation. We can improve that using *`where`*.
```haskell
bmiStatus' :: Double -> Double -> String
bmiStatus' weight height
  | bmi <= 18.5 = "You are underweight!"
  | bmi <= 25 = "You are with ideal weight!"
  | bmi <= 30 = "You are overweight!"
  | otherwise = "You are obese!"
  where bmi = weight / height ^ 2


bmiStatus’ 85 1.81
"You are overweight!"


bmiStatus’ 80 1.81
"You are with ideal weight!"


bmiStatus’ 60 1.81
"You are underweight!"


bmiStatus’ 100 1.81
"You are obese!"
```


Now we have our function simpler and faster because the calculation is done once. But we can improve it and make our function more readable and meaningful too.
```haskell
bmiStatus' :: Double -> Double -> String
bmiStatus' weight height
  | bmi <= skinny = "You are underweight!"
  | bmi <= normal = "You are with ideal weight!"
  | bmi <= fat = "You are overweight!"
  | otherwise = "You are obese!"
  where bmi = weight / height ^ 2
           (skinny, normal, fat) = (18.5, 25, 30)


```
One thing which we have to be aware and take care is that *`where`* has scope for function body. Then if the same function has two bodies and the last has one *`where`* the “variables” are just available in the second body and not in all function.
The *`where`* also can be used with *`Pattern Matching`* when we want save values in “variables”.

<br />

Today we learnt more two good features which can help us to write code in *`Haskell`*.
