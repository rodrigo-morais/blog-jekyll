---
layout: post
title: Maratona de Haskell - Vigésimo Sétimo à Vigésimo Oitavo Dia
published: true
lang: pt_BR
translation: true
---

Fala pessoal!

No último post nós vimos como construir uma *`Binary Tree Search (BST)`* a partir de uma lista. Hoje nós vamos falar sobre a função *`insert`* que pode adicionar um nodo em nossa *`BST`*.

<br />

**Relembrando BST**

Nós já sabemos como construir uma *`BST`* a partir de uma lista. Nós temos a função *`build`* e uma função auxiliar para nos ajudar. A função auxiliar tem um acumulador que seria a nossa árvore.

<!--more-->

```haskell
build' :: (Ord a, Eq a) => [a] -> Tree a -> Tree a
build' [] tree = tree
build' (x:xs) Empty = build' xs (Node x Empty Empty)
build' (x:xs) (Node a left right)
  | a >= x = build' xs (Node a (build' [x] left) right)
  | otherwise = build' xs (Node a left (build' [x] right))

build :: (Ord a, Eq a) => [a] -> Tree a
build xs = build' xs Empty

build [8,6,9,4,7,11,10,12,8,6,2,3,1]
Node 8 (Node 6 (Node 4 (Node 2 (Node 1 Empty Empty) (Node 3 Empty Empty)) (Node 6 Empty Empty)) (Node 7 Empty (Node 8 Empty Empty))) (Node 9 Empty (Node 11 (Node 10 Empty Empty) (Node 12 Empty Empty)))
```

Eu acho que podemos melhorar essas funções.

<br />

**Criar um Nodo Simples**

Primeiro de tudo vamos criar uma helper function chamada *`singleNode`* que recebe um valor e cria um nodo somente com o valor e os lados direito e esquerdo vazios.
```haskell
singleNode :: (Ord a) => a -> Tree a
singleNode x = Node x Empty Empty
```
Tão simples que é auto-explicativo.

<br />

**Inserir um Nodo na Árvore**

Agora podemos criar uma função para inserir um novo valor em uma *`BST`*. Essa função recebe uma árvore na qual queremos adicionar o valor e o valor. O output da função *`insert`* é a árvore recebida com o novo valor.
```haskell
insert :: (Ord a) => Tree a -> a -> Tree a
insert Empty x = singleNode x
insert (Node a left right) x
  | a >= x = Node a (insert left x) right
  | otherwise = Node a left (insert right x)
```

Aqui nós estamos usando a função *`singleNode`* que nós criamos acima somente para fazer nosso código mais limpo.  
A função *`insert`* é realmente simples somente procura o lugar correto para adicionar o novo valor. Para fazer isso a função navega nos lados direito e esquerdo da árvore.

<br />

**Melhorando a funcão *`build`***

Antes nós tinhamos a função *`build`* como:
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
Se dermos uma olhada nesssas funções podemos ver que elas tem algumas similaridades com a função *`insert`*. Então vamos tentar melhorar a função *`build`* usando a função *`insert`*.
```haskell
build' :: (Ord a, Eq a) => [a] -> Tree a -> Tree a
build' [] tree = tree
build' (x:xs) tree = build' xs $ insert tree x

build :: (Ord a, Eq a) => [a] -> Tree a
build xs = build' xs Empty
```
Para mim esta muito melhor. E para você?  
Nós tinhamos a função *`build'`* com 5 linhas e agora temos com apenas 2. Agora a função *`build'`* esta mais limpa e clara.

<br />

**Mais duas opções**

Além disso podemos melhorar mais nossa função *`build'`*.  
Primeiro podemos passar a função *`build'`* para dentro da função *`build`* e usa-la como uma variável interna.
```haskell
build :: (Ord a) => [a] -> Tree a
build [] = Empty
build xs = build' xs Empty
  where
    build' (y:ys) Empty = build' ys $ insert Empty y
    build' (y:ys) tree = build' ys $ insert tree y
```
Nós podemos dizer que tivemos alguma melhoria porque não necessitamos uma função auxiliar. Mas parece que não tivemos uma grande melhora.

Nós podemos melhorar um pouco mais. Vamos tentar?
```haskell
build :: (Ord a) => [a] -> Tree a -> Tree a
build [] tree = tree
build (x:xs) tree = build xs $ insert tree x
```
Agora eu acho que temos uma boa melhora. Nós removemos a função auxiliar e nossa função *`build`* tem apenas 2 linhas e esta super legível.  
O que você acha?

<br />

Dividir uma função em pequenas funções  é uma boa prática em Programação Funcional. A ideia é termos pequenas funções com apenas uma responsabilidade e funções usarem outras funções para atingirem seus objetivos. Isto foi o que fizemos com *`build`*. Nós criamos uma nova função *`insert`* que tem somente uma responsabilidade que é adicionar um novo elemento na árvore. E nós usamos a função *`insert`* em nossa função *`build`*. Isso fez nossa função *`build`* mais simples e nos deu a oportunidade de melhora-la. Porque código simples e legível é mais fácil de refatorar e temos mais confiança para fazer isso.
