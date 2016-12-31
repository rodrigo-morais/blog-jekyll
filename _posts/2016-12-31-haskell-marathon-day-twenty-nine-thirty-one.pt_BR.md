---
layout: post
title: Maratona de Haskell - Vigésimo Nono à Trigésimo Primeiro Dia
published: true
lang: pt_BR
translation: true
---

Fala galera!

No último post nós melhoramos a nossa função *`build`* e vimos algumas opções usando a função *`insert`* que nós criamos para adicionar nodos na nossa *`BST`*.  
Agora vamos ver algumas funções para encontrar um elemento na árvore ou confirmar se a árvore contém ou não um elemento.

<br />

**Recapitulando**

Primeiro vamos fazer uma rápida revisão de como chegamos até aqui.

Nós começamos criando um tipo para a nossa *`BST`*.
```haskell
data (Ord a, Eq a) => Tree a = Empty | Node a (Tree a) (Tree a)
  deriving Show
```

<!--more-->
No segundo post vimos como contruir uma *`BST`* a partir de uma lista.
```haskell
build' :: (Ord a, Eq a) => [a] -> Tree a -> Tree a
build' [] tree = tree
build' (x:xs) Empty = build' xs (Node x Empty Empty)
build' (x:xs) (Node a left right)
  | a >= x = build' xs (Node a (build' [x] left) right)
  | otherwise = build' xs (Node a left (build' [x] right))

build :: (Ord a, Eq a) => [a] -> Tree a
build xs = build' xs Empty
```

No último post criamos a função *`insert`*.
```haskell
singleNode :: (Ord a) => a -> Tree a
singleNode x = Node x Empty Empty


insert :: (Ord a) => Tree a -> a -> Tree a
insert Empty x = singleNode x
insert (Node a left right) x
  | a >= x = Node a (insert left x) right
  | otherwise = Node a left (insert right x)
```

Usando a nossa função *`insert`* nós vimos algumas opções de melhoria para a função *`build`*:
```haskell
build' :: (Ord a, Eq a) => [a] -> Tree a -> Tree a
build' [] tree = tree
build' (x:xs) tree = build' xs $ insert tree x

build :: (Ord a, Eq a) => [a] -> Tree a
build xs = build' xs Empty


build2 :: (Ord a) => [a] -> Tree a
build2 [] = Empty
build2 xs = build2' xs Empty
  where
    build2' (y:ys) Empty = build2' ys $ insert Empty y
    build2' (y:ys) tree = build2' ys $ insert tree y


build3 :: (Ord a) => [a] -> Tree a -> Tree a
build3 [] tree = tree
build3 (x:xs) tree = build3 xs $ insert tree x
```

<br />

**Encontrar um Nodo na Árvore**

Agora vamos procurar um nodo na *`BST`* e vamos retorna-lo como uma árvore.
```haskell
find :: (Ord a) => Tree a -> a -> Tree a
find Empty _ = Empty
find (Node a left right) x
  | a == x = Node a left right
  | a >= x = find left x
  | otherwise = find right x
```
Essa função retorna um nodo com os lados esquerdo e direito de acordo com o valor recebido.  
Vamos dizer que temos essa árvore:

<image src="{{site.url}}/images/bst_2.png" />

Se chamarmos a função *`find`* com o valor 6 nós receberemos essa *`BST`* como resultado:

<image src="{{site.url}}/images/bst_3.png" />

**Encontrar um Nodo na Árvore que não seja Raíz**

Legal, mas nossa *`BST`* tem dois números 6 e se nós chamarmos a função *`find`* sobre a árvore original, recebermos a nova árvore com 6 como raíz e tentarmos obter o segundo 6. Não receberemos o segundo 6 como resposta.  
Então criamos uma nova função para obter o segundo 6:
```haskell
findSub :: (Ord a) => Tree a -> a -> Tree a
findSub Empty _ = Empty
findSub (Node a left right) x
  | a >= x = find left x
  | otherwise = find right x
```
Nós podiamos fazer isso sem uma função, mas a função faz o processo mais fácil.

<br />

**Verificar se a Árvore Contém um Elemento**

Nossa última função é para verificar se uma *`BST`* contém ou não um valor:
```haskell
contains :: (Ord a) => a -> Tree a -> Bool
contains _ Empty = False
contains x (Node a left right)
  | a > x = contains x left
  | a < x = contains x right
  | otherwise = True
```
Pensando na *`BST`* anterior se chamarmos a função *`contains`* com o valor 7 ela retornará *`True`* e se chamarmos com o valor 5 ela retornará *`False`*.
