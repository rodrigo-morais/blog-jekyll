---
layout: post
title: Haskell’s marathon - Day Fifty to Fifty Three
published: true
lang: en
translation: false
---

Hey folks!!

Last post we saw how create *`records`* in *`Haskell`*. Today let’s see how to work with *`Type Synonyms`*.

<br />

**What is *`Type Synonyms`***

*`Type Synonyms`* is one way to give a new name for a type which already exist. The most popular example is the type *`[Char]`* that have a synonym *`String`*.  
If we take a look how *`String`* is declared in *`Haskell`* we can see that:
<!--more-->
```haskell
type String = [Char]
```
We can create our *`String`* from *`[Char]`*:
```haskell
type OurString = [Char]
let test = “Test” :: OurString

:t test
test :: OurString
```
In the end the keyword *`type`* just gives a new name for a type which already exist.  
We can use *`Type Synonyms`* to do our code more meaningful when necessary.

<br />

**Phonebook**

Let’s do an example called phonebook which is a list of pairs of name and telephone numbers. We can see first how to do that without *`Type Synonyms`*:
```haskell
phoneBook :: [(String, String)]
phoneBook = [("Rodrigo", "3226-9772")
            ,("Sybila", "9232-7098")
            ,("Carlos", "3765-0987")
            ]

getPhone :: [(String, String)] -> String -> Maybe String
getPhone [] _ = Nothing
getPhone (register:xs) name
  | name == fst register = Just (snd register)
  | otherwise = getPhone xs name

```
Now we can looking for a phone number in the phonebook:
```haskell
> getPhone phoneBook "Rodrigos"
Nothing

> getPhone phoneBook "Sybila"
Just "9232-7098"

> getPhone phoneBook "Rodrigo"
Just "3226-9772"
```
We have a bunch of *`String`*’s in our code, but we don’t know what is each one. We can improve that using *`Type Synonyms`*:
```haskell
type Name = String
type PhoneNumber = String
type PhoneBook = [(Name, PhoneNumber)]

phoneBook :: PhoneBook
phoneBook = [("Rodrigo", "3226-9772")
            ,("Sybila", "9232-7098")
            ,("Carlos", "3765-0987")
            ]

getPhone :: PhoneBook -> Name -> Maybe PhoneNumber
getPhone [] _ = Nothing
getPhone (register:xs) name
  | name == fst register = Just (snd register)
  | otherwise = getPhone xs name
```
Now we have three *`Type Synonyms`* which made our code much more meaningful and readable. With this code we know what is a *`PhoneBook`* and that the function *`getPhone`* needs a *`Name`* to return a *`PhoneNumber`*.

```haskell
> getPhone phoneBook "Rodrigos"
Nothing

> getPhone phoneBook "Sybila"
Just "9232-7098"

> getPhone phoneBook "Rodrigo"
Just "3226-9772"
```

<br />

*`Type Synonyms`* is important to improve the readability of our code and make it much more meaningful, but we have to be prudent and not use it for everything and just when we need to give a better understanding to other developers who are reading our code or make it more expressive.
