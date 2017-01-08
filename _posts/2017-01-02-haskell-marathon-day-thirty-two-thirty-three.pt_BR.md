---
layout: post
title: Maratona de Haskell - Trigésimo Segundo à Trigésimo Terceiro Dia
published: true
lang: pt_BR
translation: true
---

Fala galera!

No último post nós vimos algumas funções para encontrar um elemento na árvore ou confirmar se a árvore contém ou não um elemento.  
Hoje aprenderemos como calcular o tamanho e altura de uma *`BST`*.

<br />

**Revisão**

Primeiramente vamos fazer uma rápida revisão sobre encontrar elementos e confirmar se um elemento existe ou não em nossa *`BST`*.

Primeiro como encontramos um elemento em nossa árvore.
```haskell
find :: (Ord a) => Tree a -> a -> Tree a
find Empty _ = Empty
find (Node a left right) x
  | a == x = Node a left right
  | a >= x = find left x
  | otherwise = find right x
```

<!--more-->

E quando temos dois elementos repetidos, como encontramos o segundo elemento?
```haskell
findSub :: (Ord a) => Tree a -> a -> Tree a
findSub Empty _ = Empty
findSub (Node a left right) x
  | a >= x = find left x
  | otherwise = find right x
```

Vamos confirmar se o elemento existe ou não na árvore:
```haskell
contains :: (Ord a) => a -> Tree a -> Bool
contains _ Empty = False
contains x (Node a left right)
  | a > x = contains x left
  | a < x = contains x right
  | otherwise = True
```

<br />

**Calculando o Tamanho de uma *`BST`***

Uma importante funcionalidade quando estamos trabalhando com *`BST`* é obter o tamanho da árvore.  
O tamanho quer dizer o número de elementos que uma *`BST`* contém. Então vamos criar uma função para isso:
```haskell
size :: (Ord a) => Tree a -> Int
size Empty = 0
size (Node _ left right) = 1 + (size left) + (size right)
```
A função é realmente simples. Nós recebemos uma árvore e retornamos o número de elementos como um Int.  
Se a árvore é *`Empty`* deve a função *`size`* retornar o valor 0. Ao contrário se a árvore não é *`Empty`* a função *`size`* somará 1 e chamará a si própria para as sub-árvores na esquerda e direita.  

Essa função trabalha recursivamente chamando-se até encontrar um nodo *`Empty`*.
Vamos ver como ela funciona:
```haskell
> let tree = build [8,6,9,4,7,11,10,12,8,6,2,3,1]
> tree
Node 8 (Node 6 (Node 4 (Node 2 (Node 1 Empty Empty) (Node 3 Empty Empty)) (Node 6 Empty Empty)) (Node 7 Empty (Node 8 Empty Empty))) (Node 9 Empty (Node 11 (Node 10 Empty Empty) (Node 12 Empty Empty)))

> size tree
13

> let newTree = find tree 6
> newTree
Node 6 (Node 4 (Node 2 (Node 1 Empty Empty) (Node 3 Empty Empty)) (Node 6 Empty Empty)) (Node 7 Empty (Node 8 Empty Empty))

> size newTree
8
```

<br />

**Quão alto você é?**

Outra função que é realmente útil quando estamos trabalhando com *`BST`* é a função *`height`*. Esta função nos da a altura da árvore e nós podemos usa-la para balancear a mesma. Como podemos ver uma *`BST`*  não é balanceada.  
Por exemplo, se nós temos a lista em sequencia como: [3,4,5,6,7]  
Teremos essa *`BST`*:  

<image src="{{site.url}}/images/bst_4.png" />

Podemos ver que a árvore esta desequilibrada para a direita. Temos alguns algoritimos para balancear uma árvore e eles usam a função *`height`* para isso.  
Por enquanto vamos prestar atenção somente na função *`height`*.
```haskell
height :: (Ord a) => Tree a -> Int
height Empty = 0
height (Node _ left right) = (+) 1 $ max (height left) (height right)
```

Essa é uma função pequena, mas não é simples de entender.  
Primeiro se a árvore é *`Empty`* a altura é 0.  
Se a árvore não é *`Empty`* nós devemos somar um pela raíz e obter a altura máxima entre os lados esquerdo e direito. A função *`height`* mergulha na árvore até encontrar um nodo *`Empty`* e começa a contar a altura de baixo para cima. Ela funciona recursivamente.  

Vamos dizer que temos essa *`BST`*:

<image src="{{site.url}}/images/bst_3.png" />

Legal. Se chamamos a função:
```haskell
> newTree
Node 6 (Node 4 (Node 2 (Node 1 Empty Empty) (Node 3 Empty Empty)) (Node 6 Empty Empty)) (Node 7 Empty (Node 8 Empty Empty))

> height newTree
4
```

Como isso funciona?
Primeiro obtemos a altura do lado esquerdo. Então mergulhamos para a primeira árvore de baixo para cima.

<image src="{{site.url}}/images/bst_5.png" />

Na primeira árvore nós temos um nodo que é a raíz com valor 2 e com nodos para a esquerda e direita. Os nodos a esquerda e direita não tem nodos à esquerda ou direita ou eles tem nodos *`Empty`*. Os nodos *`Empty`* retornam a altura 0.  
Legal, então o nodo com o valor 1 é a raíz da sub-árvore que os lados esquerdo são *`Empty`*. Nós temos a função que trata isso:  
(+) 1 $ max (height left) (height right) => (+) 1 max 0 0 => (+) 1 0 => 1  

O mesmo ocorre com o lado direito da árvore onde a sub-árvore tem a raíz 3.  
Agora nós podemos ir para a raíz de nossa árvore que é 2. Vamos ver como isso funciona:  
(+) 1 $ max (height left) (height right) => (+) 1 $ max 1 1 => (+) 1 1 => 2  
Aqui nós obtemos a altura de nossa sub-árvore, comparamos o máximo e depois somamos 1 que vem da raíz sempre.  
Esse processo se repete em toda a árvore até alcançar a raíz.

Vamos terminar isso. Agora nós sabemos a altura do lado esquerdo de nossa sub-árvore que tem a raíz 4. O lado direito somente tem um nodo com o lado esquerdo e direito *`Empty`* e por causa disso que a altura é 1. Com isso temos essa função:  
(+) 1 $ max (height left) (height right) => (+) 1 $ max 2 1 => (+) 1 2 => 3  
Agora nós sabemos que o lado esquerdo da árvore tem a altura 3.  
O lado direito tem uma sub-árvore onde o lado esquerdo é *`Empty`* e o lado direito somente tem um nodo sozinho com altura 1 fazendo a altura da sub-árvore direita igual à 2.  
Com esse dados podemos somar a altura de nossa árvore:  
(+) 1 $ max (height left) (height right) => (+) 1 $ max 3 2 => (+) 1 3 => 4  

E temos o mesmo resultado da nossa função.
