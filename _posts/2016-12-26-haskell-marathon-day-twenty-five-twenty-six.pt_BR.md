---
layout: post
title: Maratona de Haskell - Vigésimo Quinto à Vigésimo Sexto Dia
published: true
lang: pt_BR
translation: true
---

Fala pessoal!

No último post nós falamos sobre *`Binary Tree Search (BST)`* e nós vimos como criar um tipo para trabalhar com ela e como escrever uma função simples.  
Hoje veremos como contruir uma *`BST`* a partir de uma lista.

<br />

***`BST`* Revisão**

Nós já sabemos que temos que criar um novo tipo para trabalhar com uma *`BST`*.
```haskell
data (Ord a, Eq a) => Tree a = Empty | Node a (Tree a) (Tree a)
  deriving Show
```

<!--more-->

Em nosso tipo a *`BST`* pode ter dois diferentes valores que são *`Empty`* ou *`Node a (Tree a) (Tree a)`* . O *`Empty`* é somente uma árvore vazia. E o *`Node a (Tree a) (Tree a)`* é um tronco da árvore que tem mais dois novos troncos a esquerda e direita.

Além da estrutura de dados da *`BST`* nós escrevemos uma simples função para ver se a árvore é vazia ou não.
```haskell
empty :: Tree a -> Bool
empty Empty = True
empty _ = False
```

<br />

**Construir uma Árvore**

Neste momento podemos criar uma *`BST`* manualmente como essa:
```haskell
let x = Node 8 (Node 6 (Node 4 (Node 2 (Node 1 Empty Empty) (Node 3 Empty Empty)) (Node 5 Empty Empty)) (Node 7 Empty Empty)) (Node 10 (Node 9 Empty Empty) (Node 11 Empty Empty))

x
Node 8 (Node 6 (Node 4 (Node 2 (Node 1 Empty Empty) (Node 3 Empty Empty)) (Node 5 Empty Empty)) (Node 7 Empty Empty)) (Node 10 (Node 9 Empty Empty) (Node 11 Empty Empty))

:t x
x :: (Num a, Ord a) => Tree a
```
Mas criar uma *`BST`* manualmente é muito chato e poderia ser bom se pudéssemos converter uma lista em uma árvore.  
Vamos dizer que temos esta lista: [8,6,9,4,7,11,10,12,8,6,2,3,1]  
Como seria a *`BST`* construída a partir desta lista?

<image src="{{site.url}}/images/bst_2.png" />

Esta *`BST`* é muito mais complexa que  a *`BST`* que vimos no post anterior.  
Vamos ver como contruir uma *`BST`* em *`Haskell`*:
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

Aqui a função *`build`* recebe uma lista e contrói um *`BST`*, mas essa função apenas chama a função auxiliar *`build'`*.  
A função *`build'`* irá fazer o trabalho sujo. Ela recebe uma lista, uma árvore e retorna uma árvore. A função *`build`* chama a função *`build'`* com a lista que foi recebida e uma árvore vazia.  
Com esses dados a função *`build'`* irá se chamar recursivamente.  
Vamos pensar em nossa lista acima que não esta vazia.  
Primeiramente a árvore esta vazia, então o primeiro elemento de nossa lista que é 8 seria a raíz de nossa árvore. Depois avaliamos o valor 6 que é menor que a raíz e é adicionado à esquerda. O próximo valor é 9 que é maior que a raíz e por causa disso ficará a direita.  
Os outros valores serguiram a mesma ideia.

Vamos ver a função funcionando:
```haskell
build [8,6,9,4,7,11,10,12,8,6,2,3,1]
Node 8 (Node 6 (Node 4 (Node 2 (Node 1 Empty Empty) (Node 3 Empty Empty)) (Node 6 Empty Empty)) (Node 7 Empty (Node 8 Empty Empty))) (Node 9 Empty (Node 11 (Node 10 Empty Empty) (Node 12 Empty Empty)))
```

Esta é a nossa lista como um *`BST`*

<br />

É possível fazer essa função *`build`* melhor e menor. Nos próximos posts nós trabalharemos como helper functions que nos ajudarão a reescrever a função *`build`*.
