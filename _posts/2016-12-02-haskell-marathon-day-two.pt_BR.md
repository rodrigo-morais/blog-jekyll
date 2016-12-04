---
layout: post
title: Maratona de Haskell - Segundo Dia
published: true
lang: pt_BR
translation: true
---

Hoje é o meu segundo dia na maratona de *`Haskell`* e nós vamos falar sobre o condicional IF e listas.

**Condicional (IF)**

Em *`Haskell`* como em outras linguagens nós podemos usar condicionais para produzirmos funções mais interessantes. Uma das condicionais mais famosas é o *`IF`* que nos permite testar se um valor ou clausula é verdadeiro ou não e retornar um novo valor seguindo este teste. A grande diferença entre *`Haskell`* e as outras linguagens é que *`Haskell`* nos proíbe de termos um *`IF`* sem *`ELSE`*. Isso acontece porque em *`Haskell`* todas as funções devem ter um retorno e se temos uma clausula *`IF`* sem *`ELSE`* nós podemos ter uma função sem nenhum retorno.
Vamos dar uma olhada em alguns exemplos usando *`IF`*:
```haskell
let biggerThanTen x = if x > 10 then "BIGGER" else "SMALLER"
biggerThanTen 5
SMALLER
biggerThanTen 12
BIGGER
let isOdd x = if x `mod` 2 == 0 then False else True
isOdd 2
False
isOdd 3
True
isOdd 4
False
isOdd 5
True
```
<br />

**Listas**

Em *`Haskell`* listas são estruturas de dados homogêneas, isso quer dizer que listas apenas aceitam elementos do mesmo tipo. Nós não podemos misturar números com strings em uma mesma lista.
Para criar uma lista nós devemos colocar os elementos dentro de colchetes e separados por vírgula:
```haskell
let numbers = [1,2,3,4]
numbers
[1,2,3,4]
let words = [“car”,”ball”,”gremio”]
words
[“car”, “ball”, “gremio”]
```
Provavelmente uma das mais importantes funções / ações quando nós estamos usando listas é a concatenação. Temos algumas diferentes formas de concatenar listas.
Vamos dar uma olhada!
```haskell
[1,2,3] ++ [4,5,6] -- ++ é usado para concatenar duas listas e ter uma nova lista como resultado da uniãoa
“hello” ++ “ “ ++ “world”
“hello world”
1 : [2,3,4,5] -- : é usado para adicionar um novo elemento no início de uma lista
[1,2,3,4,5]
‘A’ : “pple”
“Apple”
```

Outra importante função com listas é obter um elemento a partir de sua posição. Para fazermos isso temos que usar *`!!`* que nos permite obter o elemento.
```haskell
[3,5,2,4,1] !! 3
4
[‘h’,’e’,’l’,’l’,’o’] !! 2
‘l’
[‘h’,’e’,’l’,’l’,’o’] !! 9
*** Exception: Prelude.!!: index too large
```
Nesse exemplo podemos ver dois importantes fatos sobre as listas em *`Haskell`*. Primeiro é que todas as listas iniciam com o index 0, e segundo é que se tentarmos obter um index que não existe nós receberemos um erro como resultado.

<br />

Hoje nós demos uma olhada na condicional *`IF`* e em listas. Amanhã nós continuaremos estudando listas e o que podemos fazer com elas.
