---
layout: post
title: Maratona de Haskell - Décimo Terceiro Dia
published: true
lang: pt_BR
translation: true
---

Fala pessoal!

Ontem nós reescrevemos algumas funções standar do *`Haskell`* e como eu comentei essas funções estavam usando *`recursão`*.
Provavelmente a maioria ou a totalidade de vocês sabe o que é *`recursão`*. Mas se por acaso alguém não sabe eu vou explicar em poucas palavras.

<!--more-->

*`Recursão`* é ou acontece quando uma função chama a si mesma com diferentes parâmetros até encontrar o caso base. E o que é o caso base? Caso base é quando a função retorna o resultado e não continua a se chamar, em outras palavras quando a função não tem mais trabalho a fazer.

Um bom exemplo de *`recursão`* é *`fibonacci`*.
Como isso funciona? Bem, vamos começar pensando na assinatura de *`fibonacci`* que é uma função que recebe um número e retorna uma lista. Então *`fibonacci`* recebe um número e decompõem em uma lista até que a o número alcance o número 1. Em cada passo o número é decrescido de 1. Se o número é 1 ou 0 ele recebe o mesmo valor em uma lista. Ops, 1 ou 0? Parece que já temos nosso caso base.  
Vamos ver um exemplo:

Se *`fibonacci`* recebe o número 4 como seria?  
4 : 3 : 2 : 1 = [4,3,2,1]  
Vamos olhar por outro prisma:   
4 + (4 - 1) + ((4 - 1) - 1) + ((4 - 1) - 1) - 1) = [4,3,2,1]  
Você consegue ver a *`recursão`* neste exemplo? Nem eu.  
Vamos ver como funciona no *`Haskell`*:
```haskell
fibonacci :: Int -> [Int]
fibonacci 0 = [0]
fibonacci 1 = [1]
fibonacci x = x : fibonacci (x - 1)


fibonacci 4
[4,3,2,1]
```
Agora você pode ver a *`recursão`* e a função *`fibonacci`* chamando ela mesma.


<br />

Em programação funcional a técnica de *`recursão`* é realmente importante, diferentemente da programação imperativa nós não temos passos para seguir e por causa disso a função tem que chamar a si própria para retornar algum dado valioso ou fazer algo interessante.
