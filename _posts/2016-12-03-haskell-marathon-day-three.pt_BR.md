---
layout: post
title: Maratona de Haskell - Terceiro Dia
published: true
lang: pt_BR
translation: true
---

Fala pessoal!

Vamos continuar dando uma olhada em listas?
Ontem nós vimos como concatenar e obter elementos de listas. Hoje vamos ver outras funcionalidades que *`Haskell`* prove para listas.

<br />

**Listas aninhadas**

Isso é bem simples e obvio. Listas em *`Haskell`* podem conter números, string, booleanos e outras listas.
Vamos dar uma olhada como fazer isso:
```haskell
[[1,2,3],[4,5,6]]
[[1,2,3],[4,5,6]]
[['h','e','l','l','o'],['w','o','r','l','d']]
["hello","world"]
[[1,2,3],['h','i']]
<interactive>:43:3:
    No instance for (Num Char) arising from the literal ‘1’
    In the expression: 1
    In the expression: [1, 2, 3]
    In the expression: [[1, 2, 3], ['h', 'i']]
```
No caso de listas aninhadas a regra sobre tipos continua mandatória. Como podemos ver no último exemplo nós não podemos combinar duas listas com tipos diferentes.

<br />

**Comparando listas**

*`Haskell`* nos permite comparar listas se os seus elementos são comparáveis. Quando usamos *`<`*, *`<=`*, *`==`*, *`/=`*, *`>`* ou *`>=`* para comparar duas listas elas são comparadas em uma ordem lexicográfica. Isso significa que primeiro são comparados os dois elementos das listas, se eles forem iguais, compara-se os segundos elementos e assim por diante.
Vamos ver como a comparação funciona:
```haskell
let listA = [1,2,3]
let listB = [1,2,3]
let listC = [1,3,4]
listA == listB
True
listA /= listB
False
listA == listC
False
listA >= listC
False
listA <= listC
True
```
<br />

**Outras operações**

*`Haskell`* tem mais operações para trabalhar com listas. Vamos dar uma rápida olhada nelas:
```haskell
head [1,2,3,4,5] -- obtém o primeiro elemento de uma lista
1
tail [1,2,3,4,5] -- obtém a lista sem o primeiro elemento
[2,3,4,5]
head [] -- retorna um erro quando a lista é vazia
*** Exception: Prelude.head: empty list
tail [] -- retorna um erro quando a lista é vazia
*** Exception: Prelude.tail: empty list
tail [1] -- retorna uma lista vazia quando a lista possue apenas um elemento
[]
init [1,2,3,4] -- o oposto de tail. Retorna todos os elementos da lista menos o último
[1,2,3]
init [1] -- retorna uma lista vazia se ela possue apenas um elemento
[]
last [1,2,3] -- retorna o último elemento da lista
3
length [1,2,3,4,5] -- retorna o tamanho da lista
5
length []
0
null [1,2] -- retorna True se a lista é vazia
False
null []
True
reverse [5,4,3,2,1] -- reverte a lista
[1,2,3,4,5]
reverse [1,2,3,4,5]
[5,4,3,2,1]
take 3 [3,4,2,6,3,1,8] -- retorna o número de elemento solicitados da lista
[3,4,2]
take 30 [3,4,2,6,3,1,8]
[3,4,2,6,3,1,8]
drop 3 [3,4,2,6,3,1,8] -- remove o número de elementos informados e retorna uma nova lista
[6,3,1,8]
drop 30 [3,4,2,6,3,1,8]
[]
maximum [2,9,6,4,3,7,8] -- obtém o maior elemento da lista
9
minimum [2,9,6,4,3,7,8] -- obtém o menor elemento da lista
2
sum [2,9,6,4,3,7,8] -- soma os elementos da lista
39
product [2,9,6,4,3,7,8] -- multiplica os elementos da lista
72576
4 `elem` [2,9,6,4,3,7,8] -- verifica se o elemento existe na lista
True
1 `elem` [2,9,6,4,3,7,8]
False
```
<br />

**Intervalo de lista**

Às vezes nós temos que criar listas enormes e *`Haskell`* tem um caminho para nos ajudar com isso. Nós temos que usar o intervalo de lista. Isso é muito simples, mas realmente poderoso.
```haskell
[1..20]
[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]
['A'..'s']
"ABCDEFGHIJKLMNOPQRSTUVWXYZ[\\]^_`abcdefghijklmnopqrs"
[3,6..12]
[3,6,9,12]
[1..] -- infinite numbers
take 5 [1..] -- pega os primeiro cinco números da lista infinita
[1,2,3,4,5]
```
<br />

Hoje aprendemos alguma novas operações com listas.
