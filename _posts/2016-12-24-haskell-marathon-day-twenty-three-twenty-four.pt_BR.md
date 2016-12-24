---
layout: post
title: Maratona de Haskell - Vigésimo Terceiro à Vigésimo Quarto Dia
published: true
lang: pt_BR
translation: true
---

Fala pessoal!

Esses últimos dias estou trabalhando em alguns exercícios e queria convidar vocês a criar uma *`Binary Search Tree (BST)`* comigo.  
A *`BST`* é uma estrutura de dados que possui os dados ordenados facilitando a busca dos mesmos dentro dela. A *`BST`* segue algumas regras onde valores menores ou iguais a raíz devem ficar à esquerda e os valores maiores à direita. Por causa disso os valores em uma *`BST`* devem ser comparáveis como Int, Char e etc são.

<!--more-->

Vamos dizer que nós temos uma lista como: [5,3,6,3,2,7,1,8,9]  
Está lista criará uma árvore como essa:  

<image src="{{site.url}}/images/bst_1.png" />

Você pode ver que os números da lista estão crescendo somente para a esquerda ou direita na árvore? Neste caso nós temos uma árvore com os lados esquerdo e direito, e um monte de sub-árvores com somente o lado esquerdo ou direito.

Como criamos está árvore a partir da lista?  
Primeiramente nós obtemos o primeiro elemento da lista que seria o número 5. Depois disso obtemos o segundo elemento que é 3 e comparamos com 5. O número 3 é menor que o número 5 e por isso nós os colocamos no lado esquerdo da raíz que seria o número 5. Agora nós temos uma árvore que a raíz é o número 5, o lado esquerdo tem uma folha que é o número 3 e o lado direito esta vazio.  
Seguindo nossa lista o próximo número é 6 que é maior que a raíz 5 e deve ficar a direita. Agora nós temos uma árvore com duas folhas, uma na esquerda e outra na direita.  
Próximo valor é o 3 que é menor que a raíz 5 e deve estar a esquerda. Então nós temos que comparar como o próximo valor da esquerda que seria 3 também e por causa disso o valor deve estar a esquerda. Agora nós temos uma sub-árvore que tem a raíz 3, o lado esquerdo que é 3 e o direito que é vazio.  
Este processo aconteceu com todos os números em nossa lista e terminou criando a árvore que temos.


Agora vamos ver como criar uma *`BST`* em *`Haskell`*:
```haskell
data Tree a = Empty | Node a (Tree a) (Tree a)
  deriving Show

:t Node
Node :: a -> Tree a -> Tree a -> Tree a

:t Empty
Empty :: Tree a
```
Agora temos um tipo *`Tree a`* com dois diferentes valores que são *`Empty`* e *`Node a (Tree a) (Tree a))`*. O *`Tree`*, *`Empty`* e *`Node`* não são tipos ou valores do *`Haskell`*, mas nós criamos eles para o nosso programa. No futuro iremos falar mais sobre isso, mas por agora nós podemos pensar neles como tipos iguais Int, Char e etc.
Outro ponto é o *`deriving Show`* que nós associamos com o nosso tipo. Isso serve para podermos imprimir nossa árvore.

Agora vamos escrever uma função bem simples que diz se nossa *`BST`* esta vazia ou não. Se a *`BST`* tem o valor *`Empty`* então ela é vazia e ao contrário não.
```haskell
empty :: Tree a -> Bool
empty Empty = True
empty _ = False

let emptyTree = Empty
empty emptyTree
True

let tree = Node 3 Empty Empty
empty tree
False
```
Uma função muito simples que diz se nossa *`BST`* é vazia ou não.

