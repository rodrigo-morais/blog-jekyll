---
layout: post
title: Maratona de Haskell - Trigésimo Quarto à Quadragésimo Dia
published: true
lang: pt_BR
translation: true
---

Fala galera!

No último post nós vimos algumas funções para calcular o tamanho e altura de nossa *`Binary Search Tree (BST)`*.  
Hoje será o último post sobre os exercícios com *`BST`* e nós criaremos a função para remover nodos.

<br />

**Revisão da BST**

Vamos apenas recapitular como eram as funções *`size`* e *`height`* que trabalhamos no post anterior.

Primeiro a função *`size`* para trabalhar com uma *`BST`* que significa obter o número de elementos que existem em uma *`BST`*.
 *`BST`*.
```haskell
size :: (Ord a) => Tree a -> Int
size Empty = 0
size (Node _ left right) = 1 + (size left) + (size right)

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

<!--more-->

Uma função super direta para contar o número de nodos.

Agora vamos ver a função *`height`* que nos da a altura de uma *`BST`*.
```haskell
height :: (Ord a) => Tree a -> Int
height Empty = 0
height (Node _ left right) = (+) 1 $ max (height left) (height right)

> newTree
Node 6 (Node 4 (Node 2 (Node 1 Empty Empty) (Node 3 Empty Empty)) (Node 6 Empty Empty)) (Node 7 Empty (Node 8 Empty Empty))

> height newTree
4
```
A função parece simples, mas não é fácil de entender a computação por trás dela. Se você tem alguma dúvida eu sugiro que visite o [post](https://rodrigo-morais.github.io/pt_BR/haskell-marathon-day-thirty-two-thirty-three/) anterior.

<br />

**Remover um nodo da *`BST`***

Nós já temos funções para criar uma *`BST`* a partir de uma lista, adicionar um nodo, encontrar um nodo e avaliar se um valor existe ou não em nossa árvore. Agora temos que fazer a última função que é para remover um nodo de nossa *`BST`*.  
Vamos dizer que temos essa *`BST`*:

<image src="{{site.url}}/images/bst_6.png" />

Podemos iniciar tentando remover o nodo com o número 10. Isso é muito fácil, porque este nodo não tem outros nodos no lado esquerdo ou direito. Nós somente temos que remove-lo.  
Vamos ver como é a função *`delete`*:  
```haskell
empty :: Tree a -> Bool
empty Empty = True
empty _ = False

findSmallest :: (Ord a) => Tree a -> a
findSmallest Empty = error "Empty list"
findSmallest (Node a left _)
  | empty left = a
  | otherwise = findSmallest left

delete :: (Ord a) => Tree a -> a -> Tree a
delete Empty _ = Empty
delete (Node a left right) x
  | a == x && empty right = left
  | a == x && empty left = right
  | a == x = Node smaller left newRight
  | a >= x = Node a (delete left x) right
  | otherwise = Node a left (delete right x)
  where smaller = findSmallest right
        newRight = delete right smaller
```
A função *`delete`* usa duas helper functions para remover um nodo que são *`empty`* e *`findSmallest`*. A função *`delete`* funciona recursivamente. Vamos ver como é o processo para remover o valor 10:  
  * O primeiro valor é 8 e ele é comparado com o valor 10 que queremos remover. O número 8 é menor que 10 e o valor 10 deve estar no lado direito da árvore.
  * Move para o próximo elemento no lado direito que é 12. O número 12 é maior que 10 e a avaliação deve continuar para o lado esquerdo do nodo 12.  
  * Move para o próximo elemento no lado esquerdo que é 11. O número 11 é maior que 10 e a avaliação deve continuar para o lado esquerdo do nodo 11.  
  * Move para o próximo elemento no lado esquerdo que é 10. O número 10 é o número que estamos procurando. A primeira avaliação que a nossa função faz nesse caso é se o lado direito é vazio. E ele é. Então retornamos o lado esquerdo que neste caso é vazio também.


E temos a mesma árvore sem o nodo com valor 10.

<image src="{{site.url}}/images/bst_7.png" />

Agora vamos tentar remover o valor 12 da nossa árvore original. Mas o que faremos com os lados direito e esquerdo deste nodo se eles não são vazio? O resultado será:  

<image src="{{site.url}}/images/bst_8.png" />

A função *`delete`* remove o nodo com valor 12 e move o menor nodo da direita, que neste caso é o nodo com valor 18, para o lugar do nodo removido. Vamos ver como isso funciona:  
  * O primeiro valor é 8 e ele é comparado com o valor 10 que queremos remover. O número 8 é menor que 10 e o valor 10 deve estar no lado direito da árvore.
  * Move para o próximo elemento no lado direito que é 12. O número 12 é o número que estamos procurando. Então nós temos que procurar o menor valor no lado direito desta sub-tree.
  * Usando a helper function *`findSmallest`* nós descobrimos que o menor valor à direita é 18.
  * Recriamos a árvore colocando o nodo com o valor 18 onde o nodo com valor 12 está.

Ambos o processo e a função não são simples de entender, mas é um bom exercício para treinar *`Haskell`*.

<br />

O código para a nossa *`BST`* esta [nesse repositório](https://github.com/rodrigo-morais/haskell-exercises/blob/master/binary-tree.hs).
