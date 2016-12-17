---
layout: post
title: Maratona de Haskell - Décimo Quarto, Quinto e Sexto Dias
published: true
lang: pt_BR
translation: true
---

Fala pessoal!

Primeiramente uma explicação porque eu não escrevi os posts dos dias 14, 15 e 16 separadamente. Eu percebi que eu estava perdendo muito tempo dos meus estudos fazendo os posts e por causa disso eu irei tentar uma nova estratégia para ser mais produtivo.

<!--more-->

## Quatorze

Ok. No dia treze nós falamos sobre *`recursão`* e como isto é importante principalmente para programação funcional. Hoje vamos dar uma olhada em algumas funções padrões do *`Haskell`* que podem ser reescritas com *`recursão`*. As funções são *`replicate`*, *`take`*, *`reverse`*, *`repeat`*, *`zip`* e *`elem`*:


#### Replicate

Vamos iniciar com a função *`replicate`* que recebe um Int e outro valor. O Int é a quantidade de vezes que o outro valor será replicado.

```haskell
replicate' :: Int -> a -> [a]
replicate' 0 _ = []
replicate' n x = x : replicate' (n - 1) x

replicate' 5 3
[3,3,3,3,3]

replicate' 5 'a'
"aaaaa"
```
Nós podemos ver que *`replicate`* chama a si mesma até o valor Int atingir o número 0.

<br />

#### Take

A função *`take`* recebe um Int que é a quantidade e uma lista. A função deve retornar uma nova lista com o primeiros elementos da lista recebida de acordo com a quantidade informada.
```haskell
take' :: (Eq a) => Int -> [a] -> [a]
take' _ [] = []
take' n (x:xs)
  | n <= 0 = []
  | otherwise = x : take' (n - 1) xs

take’ 3 [1,2,3,4]
[1,2,3]

take’ 2 [1,2,3,4]
[1,2]
```

<br />

#### Reverse

A função *`reverse`* recebe uma lista e retorna a mesma na ordem oposta.
```haskell
reverse' :: [a] -> [a]
reverse' [] = []
reverse' (x:xs) = reverse' xs ++ [x]

reverse' [1,2,3,4,5]
[5,4,3,2,1]

reverse' ['a','b','c','d','e']
"edcba"
```

<br />

#### Repeat

A função *`repeat`* recebe um valor e repete o mesmo infinitamente.
```haskell
repeat' :: a -> [a]
repeat' x = x : repeat' x

take 10 $ repeat' 3
[3,3,3,3,3,3,3,3,3,3]

take 10 $ repeat' 'f'
"ffffffffff"
```

<br />

#### Zip

A função *`zip`* recebe duas listas e retorna uma lista de tuplas combinando ambas.
```haskell
zip' :: [a] -> [b] -> [(a,b)]
zip' _ [] = []
zip' [] _ = []
zip' (x:xs) (y:ys) = [(x,y)] ++ zip' xs ys

zip' [1,2,3] [6,7,8]
[(1,6),(2,7),(3,8)]

zip' ['a','b','c'] [6,7,8]
[('a',6),('b',7),('c',8)]

```

<br />

#### Elem

A função *`elem`* recebe um valor e uma lista e retorna um booleano que diz se o valor existe na lista ou não.
```haskell
elem' :: (Eq a) => a -> [a] -> Bool
elem' _ [] = False
elem' x (y:ys)
  | x == y = True
  | otherwise = elem' x ys

3 [1,2,4,3,5,8,6]
True

elem' 7 [1,2,4,3,5,8,6]
False
```

Todas as funções anteriores estão usando *`recursão`* chamando a si próprias para retornar o resultado.

<br />

Legal. Agora vamos ver uma função mais complexa. Se você estudou ciência da computação você já trabalhou com uma função *`Quick Sort`* que recebe uma lista desordenada e a retorna ordenada.

Vamos dar uma olhada no seu código:
```haskell
quickSort' :: (Ord a) => [a] -> [a]
quickSort' [] = []
quickSort' (x:xs) =
  let
    smaller = [ a | a <- xs, a < x ]
    bigger = [ a | a <- xs, a > x ]
    same = [ a | a <- xs, a == x ]
  in
    (quickSort' smaller) ++ [x] ++ same ++ (quickSort bigger)

quickSort [2,4,1,6,3,7,5,2,4]
[1,2,2,3,4,4,5,6,7]
```
Esta é uma simples solução, nós estamos pegando o primeiro elemento e checando quais os elementos da lista são menores, iguais ou maiores. Os menores valores ficarão no lado esquerdo do elemento que estamos avaliando e os elementos com o mesmo valor ou maiores ficarão no lado direito. A *`recursão`* é aplicada duas vezes, uma para os menores e outra para os maiores. Nós estamos usando *`let..in`* para fazer a função mais legível.

<br />

## Quinze

No décimo quinto dia eu estudei *`higher-order function`* que é um importante assunto em programação funcional e nos permite fazer muito mais coisas e nos da muito mais poder.  
Nós já vimos alguns exemplos com *`higher-order function`* e isso não é nada mais que passar uma função como parâmetro para uma função. Os dois mais famosos exemplos são as funções *`map`* e *`filter`*.

A função *`map`*  recebe uma função como parâmetro e uma lista e aplica a função para cada elemento da lista retornando uma nova lista.
```haskell
map (*2) [1,2,3,4,5]
[2,4,6,8,10]

map (+2) [1,2,3,4,5]
[3,4,5,6,7]
```

<br />

A função *`filter`* recebe uma função que retorna um booleano e uma lista. O resultado da função *`filter`* é uma nova lista com todos elemento da lista recebida que foram aplicados a função e retornaram True.
```haskell
filter (>= 3) [1,2,3,4,5,6]
[3,4,5,6]

filter (<= 3) [1,2,3,4,5,6]
[1,2,3]
```

<br />

Além de *`higher-order function`* eu estudei *`curried function`*  que é uma função que recebe sempre apenas um parâmetro e retorna uma função. Todas as funções em *`Haskell`* somente recebem um parâmetro. Mas nós trabalhamos com um monte de funções que recebem mais de um parâmetro.  
Como isso é possível? *`Haskell`* usa *`curried functions`* para fazer isso possível e prove um "syntax sugar" onde nós podemos trabalhar com multiplos parâmetros.  
Vamos dar uma olhada:
```haskell
:t map
map :: (a -> b) -> [a] -> [b]

map (*2) [1,2,3,4,5]
[2,4,6,8,10]

let x = map (*2)
:t x
x :: Num b => [b] -> [b]

x [1,2,3,4,5]
[2,4,6,8,10]
```
Aqui nós podemos ver isto. Primeiro nós vemos o tipo da função *`map`* que é: *`map :: (a -> b) -> [a] -> [b]`*  
Se rodamos essa expressão *`map (*2) [1,2,3,4,5]`* nós temos o resultado *`[2,4,6,8,10]`*.  
O que esta acontecendo? Primeiro *`Haskell`* esta rodando somente *`map`* como primeiro parâmetro: *`map (*2)`* e retornando uma nova função. E depois roda a nova função com o segundo parâmetro.  
Nós fizemos um exemplo acima usando uma variável para mostrar.

<br />

## Dezesseis

No décimo sexto dia eu fiz alguns exercícios para praticar *`higher-order function`* reescrevendo algumas funções padrões do *`Haskell`* como *`zipWith`*, *`flip`*, *`map`* e *`filter`*.

Abaixo as funções *`map`* e *`filter`* reescritas.
```haskell
map' :: (a -> b) -> [a] -> [b]
map' _ [] = []
map' f (x:xs) = f x : map' f xs


filter' :: (a -> Bool) -> [a] -> [a]
filter' _ [] = []
filter' f (x:xs)
  | f x = x : filter' f xs
  | otherwise = filter' f xs
```

<br />

E eu dei uma olhada em *`Lambda functions`* que são funções anônimas que são usadas apenas uma vez.
```haskell
map (\x -> x + 3) [1,2,3,4]
[4,5,6,7]
```

A parte do código acima com a expressão *`(\x -> x + 3)`* é uma *`lambda function`*. Eu irei escrever um ou mais posts sobre *`Lambda Functions`* porque eu penso que é a forma mais fácil de aprender programação funcional.
