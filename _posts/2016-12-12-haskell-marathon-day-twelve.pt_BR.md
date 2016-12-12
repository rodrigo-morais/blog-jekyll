---
layout: post
title: Maratona de Haskell - Décimo Segundo Dia
published: true
lang: pt_BR
translation: true
---

Fala pessoal!


Hoje nós contiamos fazendo exercícios. Ontem fizemos alguns exercícios e no exercício nove nós usamos duas funções standard do *`Haskell`* que foram *`takeWhile`* e *`dropWhile`*. Agora vamos fazer algo levemente diferente, nós vamos criar nossas próprias *`takeWhile`* e *`dropWhile`* e usa-las no exercício nove.

<!--more-->


Vamos iniciar com *`takeWhile`* porque depois *`dropWhile`* será bem parecida.
A função *`takeWhile`* obtém os elementos de uma lista equanto eles respeitam a função informada.
```haskell
takeWhile (=='a') ['a', 'a', 'a', 'a', 'b', 'c', 'c', 'a', 'a', 'd', 'e', 'e', 'e', 'e']
"aaaa"


takeWhile (<= 3) [1,2,3,4,5,6]
[1,2,3]
```
Ok. Quando criamos uma função é sempre mais fácil começar com seu comportamento. Em *`Haskell`* nós fazemos isso pensando na assinatura da função.  
Como é a assinatura de *`takeWhile`*? Bem, a função recebe uma função e uma lista. E o resultado é uma lista.  
Ok, e como é essa função? A função recebe um elemento e retorna um booleano.
Ótimo, parece que já temos a assinatura.
```haskell
takeWhile’ :: (a -> Bool) -> [a] -> [a]
```
A *`(a -> Bool)`* é a nossa função que recebemos o elemento *`a`* e retorna um booleano. *`[a]`* é a lista que recebemos e o último *`[a]`* é a lista que retornamos.

Legal. O próximo passo é pensar nas exceções que no nosso caso é quando recebemos uma lista vazia. O que fazemos com uma lista vazia? Nada. Então vamos escrever isso:
```haskell
takeWhile’ :: (a -> Bool) -> [a] -> [a]
takeWhile’ _ [] = []
```
Neste caso a função não é importante e nós estamos usando o *`_`* para isso.
Agora vamos para a parte mais importante da função. Vamos pensar, o que acontece quando o primeiro elemento da lista é verdadeiro para a nossa função? Neste caso queremos retornar ele e continuar verificando a lista.
```haskell
takeWhile’ :: (a -> Bool) -> [a] -> [a]
takeWhile’ _ [] = []
takeWhile’ f (x:xs) =
    If f x then
        x: takeWhile’ f xs
```
Simples assim:

Ok. Mas quando a função retorna falso para o nosso elemento? Bem, neste caso nós não temos que retornar o elemento e parar de avaliar a lista.
```haskell
takeWhile’ :: (a -> Bool) -> [a] -> [a]
takeWhile’ _ [] = []
takeWhile’ f (x:xs) =
    If f x then
        x: takeWhile’ f xs
    else
        []
```
E se testarmos:
```haskell
takeWhile’ (=='a') ['a', 'a', 'a', 'a', 'b', 'c', 'c', 'a', 'a', 'd', 'e', 'e', 'e', 'e']
"aaaa"


takeWhile’ (<= 3) [1,2,3,4,5,6]
[1,2,3]
```
Funciona. Mas podemos melhorar a função usando *`Guards`*. Vamos testar?
```haskell
takeWhile'' :: (a -> Bool) -> [a] -> [a]
takeWhile'' _ [] = []
takeWhile'' f (x:xs)
  | f x = x : takeWhile' f xs
  | otherwise = []


takeWhile’’ (=='a') ['a', 'a', 'a', 'a', 'b', 'c', 'c', 'a', 'a', 'd', 'e', 'e', 'e', 'e']
"aaaa"


takeWhile’’ (<= 3) [1,2,3,4,5,6]
[1,2,3]
```
Funciona também. E a função parece melhor. O que você acha?


Ok. Agora vamos ver o *`dropWhile`*. Esta função recebe como parâmetro uma função e uma lista e retorna outra lista. Igual ao *`take While`*, não è?
E tem mais, se a lista recebida é vazia a função retorna uma lista vazia também.
```haskell
dropWhile’ :: (a -> Bool) -> [a] -> [a]
dropWhile’ _ [] = []
```
O que irá mudar no *`dropWhile`* é a última parte que tem um comportamento diferente do *`takeWhile`*. No *`dropWhile`* nós queremos remover os elementos se eles são verdadeiro de acordo com a função recebida como parâmetro. E se o elemento é falso nós paramos de avaliar a lista e retornamos ela com o elemento.
```haskell
dropWhile'' :: (a -> Bool) -> [a] -> [a]
dropWhile'' _ [] = []
dropWhile'' f (x:xs)
  | f x = dropWhile' f xs
  | otherwise = x:xs


dropWhile'' (<= 3) [1,2,3,4,5,6]
[4,5,6]


dropWhile'' (=='a') ['a', 'a', 'a', 'a', 'b', 'c', 'c', 'a', 'a', 'd', 'e', 'e', 'e', 'e']
"bccaadeeee"
```
Funciona também.

Agora nós podemos retornar para o exercício nove que trabalhamos ontem e substituir as funções standard pelas nossas.


A descrição do exercício é: Pack consecutive duplicates of list elements into sublists. If a list contains repeated elements they should be placed in separate sublists.


E o exemplo é:
```haskell
pack ['a', 'a', 'a', 'a', 'b', 'c', 'c', 'a',  'a', 'd', 'e', 'e', 'e', 'e']
["aaaa","b","cc","aa","d","eeee"]
```
Com nossas novas funções:
```haskell
pack :: (Eq a) => [a] -> [[a]]
pack [] = []
pack (x:xs) = (x: takeWhile’’ (==x) xs) : (pack $ dropWhile’’ (==x) xs)


pack ['a', 'a', 'a', 'a', 'b', 'c', 'c', 'a',  'a', 'd', 'e', 'e', 'e', 'e']
["aaaa","b","cc","aa","d","eeee"]
```
E a função *`pack`* continua funcionando com as nossas funções.

<br />

Para reescrever as funções *`takeWhile`* e *`dropWhile`* nós tivemos que usar duas técnicas chamadas *`recursion`* e *`high order function`* que serão estudadas nos próximos dois cápitulos do [livro](http://learnyouahaskell.com/) que estamos acompanhando.
