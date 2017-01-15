---
layout: post
title: Haskell’s marathon - Day Forty One to Forty Two
published: true
lang: en
translation: true
---

Hey folks!

We finished our exercises with a *`Binary Search Tree (BST)`* in the last post and now we are back to still follow the [book](http://learnyouahaskell.com/) which we are following.  
Today let’s start to talk about modules in *`Haskell`*.

<br />

**What are modules?**

Well, modules are files where we can define functions, types and types classes.  
A module has a bunch of definitions and can export just some of them. It is the same idea of private and public in Object-oriented.  

<!--more-->

The split of code in modules is a good signal and give us some advantages. First should be the reusability, if we have some functions and types which can be used for other modules is a good idea to put them by similarity in the same module to make easy reuse them. Another benefit is the maintainability because if the relationed functions and types are in the same module is easier to take care of them.

<br />

**Importing a module**

Let’s say that we want use a function from a specific module as *`nub`* function from *`Data.List`* module. The *`nub`* function remove duplicate values from a list. To use it we have to import the module.  
Let’s see how we do the import:
```haskell
import Data.List
```
With this line we are importing all functions and types that *`Data.List`* module export.  
Now we can use the function *`nub`*.
```haskell
Data.List> nub [1,1,2,3,1,4,2,5,2,3,4,6]
[1,2,3,4,5,6]
```
And everything works ok. If we don’t import the module we receive an error:
```haskell
> nub [1,1,2,3,1,4,2,5,2,3,4,6]
<interactive>:2:1: Not in scope: ‘nub’
```

<br />

**Import just some functions**

When we use *`import`* as above we are importing all functions from module. To import just the functions that we need we have to say to *`Haskell`* which are the functions that we want like that:
```haskell
import Data.List (nub, sort)
```
Now we just imported the functions *`nub`* and *`sort`* and all other functions from *`Data.List`* module are not available to use.

<br />

**Get rid of some functions**

As you can choose some functions to import is possible to do the opposite and choose some to not import. For to do this is pretty simple:
```haskell
import Data.List hiding (nub)

> nub [1,1,2,3,1,4,2,5,2,3,4,6]
<interactive>:2:1: Not in scope: ‘nub’
```
And now we have all functions from *`Data.List`* module less the *`nub`* function.

<br />

**Qualifying modules**

Sometimes two different modules having the same name of function or our project has the same name of function that the module which we are importing has. In this case *`Haskell`* gives us the opportunity to qualify the imported module to still using the same function.
```haskell
> import qualified Data.List as L

L> L.nub [1,1,2,3,1,4,2,5,2,3,4,6]
[1,2,3,4,5,6]
```
And now we can use the letter *`L`* to access the functions from the module.

<br />

Today we saw how import modules in *`Haskell`*.  
Next posts we continue take a looking in how modules work in *`Haskell`*.
