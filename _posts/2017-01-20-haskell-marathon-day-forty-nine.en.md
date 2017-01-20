---
layout: post
title: Haskell’s marathon - Day Forty Nine
published: true
lang: en
translation: false
---

Hey folks!

Last post we saw how export our own data types with *`modules`*. Today let’s see how to handle with records as data type. 

<br />

**Person’s data type**

If our software needs a data type as *`Person`* to handle with person's data. Let’s say that we are working with a register in a clinic or any other silly example where we need a person's representation. As we saw till now we can create a data type with some parameters like:
```haskell
data Person = Person String String Int String

> :t Person
Person :: String -> String -> Int -> String -> Person
```
<!--more-->
Now we have a data type *`Person`* which receives a first name, last name, age and address. We can create functions to handle with our data type to get some informations.
```haskell
data Person = Person String String Int String

firstName :: Person -> String
firstName (Person firstName _ _ _) = firstName

lastName :: Person -> String
lastName (Person _ lastName _ _) = lastName

age :: Person -> Int
age (Person _ _ age _) = age

address :: Person -> String
address (Person _ _ _ address) = address

> let person = Person "Rodrigo" "Morais" 37 "Winterfeld 58"

> firstName person
"Rodrigo"
*Main> lastName person
"Morais"
*Main> age person
37
*Main> address person
"Winterfeld 58"
```
We have two problems here which we can solve with record. First one is that the *`String`* type doesn’t say what is the data which we need when we are building the data type *`Person`*. The second problem is have to write these bunch of functions to get the data from the data type *`Person`*.

<br />

**Records**

Using records we can improve that and make our data type more readable.  
Let’s see:
```haskell
data Person = Person { firstName :: String
                     , lastName :: String
                     , age :: Int
                     , address :: String
                     } deriving Show

let person = Person {firstName="Rodrigo", lastName="Morais", age=37, address="Winterfeld 58"}
> person
Person {firstName = "Rodrigo", lastName = "Morais", age = 37, address = "Winterfeld 58"}
```
Cool. Our first problem was solved. Now we put name to each parameter and we know what is each one.  

We removed all functions that we created before as *`firstName`*, *`age`* and *`address`*, but with *`records`* we can still use them:
```haskell
> firstName person
"Rodrigo"

> age person
37
> address person
"Winterfeld 58"
```

<br />

Use *`record`* when we have a structured data type with a lot of parameters is a good idea, beyond that we gain some functions for free.  
You should use *`records`* when it makes sense for your problem.
