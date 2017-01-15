---
layout: post
title: Haskell’s marathon - Day Forty Three to Forty Five
published: true
lang: en
translation: true
---

Hey folks!

Last post we saw how import modules and now we will see how create our own modules.  

How we saw in the last post create a module to put functions and types that work toward a similar purpose is a good practice.

<br />

**Create a module**

Create a new module is pretty easy we just have to put this line of code on the top of our file:
<!--more-->
```haskell
module BST where
```
This is the syntaxe, we used the word *`module`*, the name of the module that we wish and the word *`where`*.  
In this example we are creating a module for the *`BST`* which we worked some posts ago.

<br />

**Using the module**

To use the module in this case is a little different because we have to load the file. Usually the modules are installed in *`Haskell`* when we install a new library so we just need import them. In our case we are working with a local module then we have to load it first.
```haskell
Prelude> :l code/binary-tree.hs

code/binary-tree.hs:1:14: Warning:
    -XDatatypeContexts is deprecated: It was widely considered a misfeature, and has been removed from the Haskell language.
[1 of 1] Compiling BST              ( code/binary-tree.hs, interpreted )
Ok, modules loaded: BST.

*BST> :m

Prelude> import BST

Prelude BST> BST.build [5,4,6,8,3,2,9]
Node 5 (Node 4 (Node 3 (Node 2 Empty Empty) Empty) Empty) (Node 6 Empty (Node 8 Empty (Node 9 Empty Empty)))
Prelude BST>
```
First we load the file using the command *`:l`* and the name of the file. In this moment the module that exist in this file is loaded. Just to confirm this we can notice that the command line changed the text *`Prelude`* to *`BST`*.  
Second step we just remove the loaded module with the command *`:m`*.  
In the last step we import our module as we saw in the last post and we can use its functions.

<br />

**Choosing public functions**

In the example above all functions from our module are available. We can change that and just export the functions that we want should be public. If we try use *`build’`* with the approache above we can.
```haskell
Prelude BST> BST.build' [5,4,6,8,3,2,9] Empty
Node 5 (Node 4 (Node 3 (Node 2 Empty Empty) Empty) Empty) (Node 6 Empty (Node 8 Empty (Node 9 Empty Empty)))
```

Now let’s say to our module which functions should be public:
```haskell
module BST
( build
, build2
, build3
, insert
, find
, findSub
, contains
, size
, height
, delete
) where
```
With this we say to *`Haskell`* what are the functions that must be public.  

If we import and try use the *`build’`* function again we will receive an error:
```haskell
Prelude> :l code/binary-tree.hs

code/binary-tree.hs:1:14: Warning:
    -XDatatypeContexts is deprecated: It was widely considered a misfeature, and has been removed from the Haskell language.
[1 of 1] Compiling BST              ( code/binary-tree.hs, interpreted )
Ok, modules loaded: BST.

*BST> :m

Prelude> import BST

Prelude BST> BST.build' [5,4,6,8,3,2,9] Empty

<interactive>:26:1:
    Not in scope: ‘BST.build'’
    Perhaps you meant one of these:
      ‘BST.build’ (imported from BST), ‘BST.build2’ (imported from BST),
      ‘BST.build3’ (imported from BST)

<interactive>:26:28: Not in scope: data constructor ‘Empty’

Prelude BST> BST.build [5,4,6,8,3,2,9]
Node 5 (Node 4 (Node 3 (Node 2 Empty Empty) Empty) Empty) (Node 6 Empty (Node 8 Empty (Node 9 Empty Empty)))
```
But the *`build`* function is available to us because we said that it is public.

<br />

The *`BST`* with a module is in my [GitHub](https://github.com/rodrigo-morais/haskell-exercises/blob/master/binary-tree.hs).  
Now we already know how to create and import modules in *`Haskell`*.
