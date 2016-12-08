---
layout: post
title: Maratona de Haskell - Oitavo Dia
published: true
lang: pt_BR
translation: true
---

Fala pessoal!

<br />

Hoje vamos falar de *`Pattern Matching`* uma das melhores funcionalidades em *`Functional Programming`* na minha opinião.

Como a maioria das linguagens funcionais *`Haskell`* tem *`Pattern Matching`* que faz nossas vidas muito mais fácil apra criar funções com diferentes ações dependendo do que é recebido. *`Pattern Matching`* é sobre avaliar dados e desconstrui-los de acordo com seus padrões.
A ideia atrás de *`Pattern Matching`* é fazer nossos programas mais simples e legíveis. Vamos mergulhar em alguns exemplos e entender o porque.

<!--more-->

Nós podemos iniciar com uma função que recebe um número e se este número for 5 então retornamos o mês de "Maio" e se o número é diferente retorna uma mensagem "it is not a valid month". Como nós implementamos isso como uma linguagem que estamos acostumados?
```haskell
month :: Int -> String
month a =
  if a == 5 then
    "May"
  else
    "it is not a valid month"


month 5
“May”
month 6
"it is not a valid month"
```
Ok. Um simples *`IF`* pode resolver o problema, mas e se nós queremos obter “June”, “July” e “August”?
```haskell
month :: Int -> String
month a =
  if a == 5 then
    "May"
  else if a == 6 then
    "June"
  else if a == 7 then
    "July"
  else if a == 8 then
    "August"
  else
    "it is not a valid month"


month 6
"June"
month 7
"July"
month 8
“August”
month 9
"it is not a valid month"
```
A solução do *`IF`*  continua funcionando, mas é muito feia. Imagine se a função retornar todos os meses.  
Quando usamos *`Pattern Matching`* em uma função podemos criar um corpo para cada padrão fazendo a função mais simples e legível. Vamos ver:
```haskell
month' :: Int -> String
month' 5 = "May"
month' 6 = "June"
month' 7 = "July"
month' 8 = "August"


month 5
"May"
month 6
"June"
month 7
"July"
month 8
“August”
month 9
"*** Exception: code/patter_matching.hs:(17,1)-(20,19): Non-exhaustive patterns in function month'
```
Muito melhor que a versão do *`IF`*. O que você acha?  
Preste atenção que cada mês é um novo corpo de função.


Ok. Mas onde esta o *`ELSE`* final para os meses que não existem?  
Bem, *`Pattern Matching`* tem uma funcionalidade chamada *`catchall`* que é o mesmo que o *`ELSE`* final. No exemplo acima nós vimos a função falhando porque nós não temos o *`catchall`*.
```haskell
month' :: Int -> String
month' 5 = "May"
month' 6 = "June"
month' 7 = "July"
month' 8 = "August"
month' _ = "it is not a valid month"


month 9
"it is not a valid month"
```
Aqui para o *`catcall`* nós estamos usando o underscore (_) mas nós podemos usar qualquer outra letra, simbolo ou palavra. Underscore é somente um padrão do *`Haskell`*.

Outro importante ponto é a ordem das funções. Se nós temos as funções em uma ordem incorreta é possível termos um bug. No exemplo dos meses se o *`catchall`* esta antes de um mês, este mês nunca será chamado porque o *`catchall`* pega todos os casos.
```haskell
month' :: Int -> String
month' 5 = "May"
month' _ = "it is not a valid month"
month' 6 = "June"
month' 7 = "July"
month' 8 = "August"


*Main> :l code/patter_matching.hs
[1 of 1] Compiling Main             ( code/patter_matching.hs, interpreted )


code/patter_matching.hs:17:1: Warning:
    Pattern match(es) are overlapped
    In an equation for ‘month'’:
        month' 6 = ...
        month' 7 = ...
        month' 8 = ...
Ok, modules loaded: Main.


month' 5
“May”
month' 6
"it is not a valid month"
month' 9
"it is not a valid month"
```

Nós podemos usar o *`Pattern Matching`* com *`Tuples`* também. Se nós queremos somar duas *`Tuples`* como podemos fazer?  
```haskell
points :: (Int, Int) -> (Int, Int) -> (Int, Int)
points (a1, b1) (a2, b2) = (a1 + a2, b1 + b2)


points (2, 5) (7, 1)
(9,6)
```
Neste caso nós não teremos o *`catchall`* porque o primeiro padrão pega todos os casos.  
Outro exemplo com *`Tuples`* pode ser criar funções para trios. Nós já temos as funções *`fst`* e *`snd`* para pares, mas nós não temos nenhuma função para trios. Nós podemos criar então:
```haskell
first :: (a, b, c) -> a
first (a, _, _) = a


second :: (a, b, c) -> b
second (_, b, _) = b


third :: (a, b, c) -> c
third (_, _, c) = c


first (1,2,3)
1
second (1,2,3)
2
third (1,2,3)
3


``` 

E o mais importante, nós podemos usar *`Pattern Matching`* com listas que é provavelmente onde iremos usar mais esta técnica. Nós vimos anteriormente as funções *`head`* e *`tail`* que podem ser usadas com listas. Vamos reescreve-las:
```haskell
head' :: [a] -> a
head' (x:_) = x


tail' :: [a] -> [a]
tail' (_:xs) = xs


head' [1,2,3]
1
tail' [1,2,3]
[2,3]


head' []
*** Exception: code/patter_matching.hs:39:1-15: Non-exhaustive patterns in function head'


tail' []
*** Exception: code/patter_matching.hs:42:1-17: Non-exhaustive patterns in function tail'
``` 
Aqui podemos ver que as funções estão funcionando quando recebemos uma lista com elementos, mas quando a lista esta vazia as funções quebram. Vamos resolver isso.

```haskell
head' :: [a] -> a
head' [] = error "list is empty"
head' (x:_) = x


tail' :: [a] -> [a]
tail' [] = [


head' [1,2,3]
1


tail' [1,2,3]
[2,3]


head' []
*** Exception: list is empty


tail' []
[]
```
Agora esta tudo funcionando, nós demos duas diferentes soluções para cada função. Para *`head`* estamos chamando um erro quando receboms uma lista vazia porque não temos um elemento para retornar, por outro lado para a função *`tail`* nós estamos retornando uma lista vazia quando recebemos uma lista vazia porque o resto de nada é nada.


Além disso temos uma curiosidade nessa implementação, nós podemos ver que na função *`head`* nós recebemos a lista como *`(x:_)`* e na função *`tail`* como *`(_:xs)`*. Isso acontece porque em *`Haskell`* nós podemos representar listas com *`x:xs`* onde *`x`* é o primeiro elemento e *`xs`* é o resto.  
Um exemplo pode ser a lista *`[1,2,3,4]`* que pode ser representada como *`(1:(2:(3:(4))))`*. Neste caso *`1`* é o *`x`* e *`(2:(3:(4)))`* é o *`xs`*.

<br />

*`Pattern Matching`* é uma funcionalidade especial na programação funcional porque faz o código mais simples e legível. Eu posso dizer que é a minha funcionalidade favorita. Prepare-se porque você vai trabalhar bastante com *`Pattern Matching`* quando você estiver usando *`Functional Programming`*.
