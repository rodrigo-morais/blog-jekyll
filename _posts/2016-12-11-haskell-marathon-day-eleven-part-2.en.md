---
layout: post
title: Haskell's Marathon - Day Eleven - Part 2
published: true
lang: en
translation: true
---

Hey folks!


After the review which we did before I think is a good idea to do some exercises. I worked in a list of exercises called [99 questions](https://wiki.haskell.org/99_questions/1_to_10).
I worked in the ten first exercises, let’s take a look in some of them:

<!--more-->
<br />

**Exercise Two**


The description of exercise is: Find the last but one element of a list.

And this is the example:
```haskell
myButLast [1,2,3,4]
3

myButLast ['a'..'z']
'y'
```
Ok, how we saw in the third day we have the function *`last`* to get the last element of the list, but here we need get the element before the last one.
If we have a list as [1,2,3,4,5] we have to return the number 4. To do that we have some functions to help us, one is *`reverse`* which revert the list order. Another one is *`!!`* which return the element in the index informed. Remember *`Haskell`* start a list with index 0.
If we revert and get the index 1 it will work.
```haskell
myButLast :: [a] -> a
myButLast xs = reverse xs !! 1


myButLast [1,2,3,4]
3

myButLast ['a'..'z']
'y'
```

<br />

**Exercise Six**


The description of exercise is: Find out whether a list is a palindrome. A palindrome can be read forward or backward; e.g. (x a m a x).

And this is the example:
```haskell
isPalindrome [1,2,3]
False


isPalindrome "madamimadam"
True


isPalindrome [1,2,4,8,16,8,4,2,1]
True
```
It has a pretty simple solution, but it is a very famous challenge even in job interviews.
We just need to compare the list which we receive with the same list reverted.
```haskell
isPalindrome :: (Eq a) => [a] -> Bool
isPalindrome xs = xs == reverse xs


isPalindrome [1,2,3]
False


isPalindrome "madamimadam"
True


isPalindrome [1,2,4,8,16,8,4,2,1]
True
```
We just have to pay attention that this function implement the *`type class`* of equality.

<br />

**Exercise Eight**


The description of exercise is: Eliminate consecutive duplicates of list elements.
If a list contains repeated elements they should be replaced with a single copy of the element. The order of the elements should not be changed.

And this is the example:
```haskell
compress "aaaabccaadeeee"
"abcade"
```
I started that using an auxiliary function which works:
```haskell
compress :: (Eq a) => [a] -> [a]
compress [] = []
compress (x:[]) = [x]
compress (x:xs) = x : (compress $ (cleanRepeated x xs))


cleanRepeated :: (Eq a) => a -> [a] -> [a]
cleanRepeated _ [] = []
cleanRepeated x (y:ys) = if x == y then cleanRepeated x ys else y : ys


compress "aaaabccaadeeee"
"abcade"
```


But the solutions was not good enough. Then combining *`Guards`* and *`as-pattern`* the function becomes simpler:
```haskell
compress' :: (Eq a) => [a] -> [a]
compress' (x:xs@(y:_))
  | x == y = compress xs
  | otherwise = x : compress xs


compress "aaaabccaadeeee"
"abcade"
```

<br />

**Exercise Nine**


The description of exercise is: Pack consecutive duplicates of list elements into sublists. If a list contains repeated elements they should be placed in separate sublists.

And this is the example:
```haskell
pack ['a', 'a', 'a', 'a', 'b', 'c', 'c', 'a',  'a', 'd', 'e', 'e', 'e', 'e']
["aaaa","b","cc","aa","d","eeee"]
```
We already saw the functions *`take`* and *`drop`* which receive a number of the elements to take or drop. They have siblings called *`takeWhile`* and *`dropWhile`* which receive a function instead of a number.
```haskell
take 5 ['a', 'a', 'a', 'a', 'b', 'c', 'c', 'a',  'a', 'd', 'e', 'e', 'e', 'e']
"aaaab"


drop 5 ['a', 'a', 'a', 'a', 'b', 'c', 'c', 'a',  'a', 'd', 'e', 'e', 'e', 'e']
"ccaadeeee"


takeWhile (=='a') ['a', 'a', 'a', 'a', 'b', 'c', 'c', 'a',  'a', 'd', 'e', 'e', 'e', 'e']
"aaaa"


dropWhile (=='a') ['a', 'a', 'a', 'a', 'b', 'c', 'c', 'a',  'a', 'd', 'e', 'e', 'e', 'e']
"bccaadeeee"
```
With these functions is easy solve the problem:
```haskell
pack :: (Eq a) => [a] -> [[a]]
pack [] = []
pack (x:xs) = (x: takeWhile (==x) xs) : (pack $ dropWhile (==x) xs)


pack ['a', 'a', 'a', 'a', 'b', 'c', 'c', 'a',  'a', 'd', 'e', 'e', 'e', 'e']
["aaaa","b","cc","aa","d","eeee"]
```

<br />
<br />

Those are the exercises that I guess were the most difficult to solve for the knowledge which we have till now. For the next days I’ll work in more exercises.
