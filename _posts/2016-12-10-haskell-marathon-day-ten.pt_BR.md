---
layout: post
title: Haskell's Marathon - Day Ten
title: Maratona de Haskell - Décimo Dia
published: true
lang: pt_BR
translation: true
---

Fala pessoal!


Hoje vamos falar sobre duas diferentes formas de trabalhar com *`Pattern Matching`* que são *`let..in`* e *`case..of`*.


Nós já vimos um pouco sobre *`let..in`* no primeiro dia quando nós o usamos para criar "variáveis" *`GHCI`*, mas podemos usa-las levemente diferente.
<!--more-->
```haskell
let a = 5
5 * 5
25


let add a b = a + b
add 5 4
9


let add' a b = a + b in add' 5 4
9
```


Ao invés de usar o *`where`* nós podemos usar o *`let..in`* e colocar a "variável" no topo.
```haskell
cylinder :: Double -> Double -> Double
cylinder r h =
  let
    sideArea = 2 * pi * r * h
    topArea = pi * r ^ 2
  in
    sideArea + 2 * topArea


cylinder 8 10
904.7786842338604
```
Diferentemente do *`where`* o *`let..in`* é uma expressão e pode ser usado em qualquer lugar, pelo outro lado ele tem scopo somente onde é definido e nós não podemos usa-lo com *`Guards`* por exemplo, Vamos ver um exemplo de onde podemos usar *`let..in`*.
```haskell
4 + let b = 5 in 5 + b + 2


[let square x = x * x in (square 2, square 3, square 4)]
[(4,9,16)]
```
Quando dizemos que *`let..in`* é uma expressão queremos dizer que ele tem um valor e por causa disso podemos usa-lo em qualquer lugar.


Podemos usar o *`let..in`* em list comprehension também. Com *`let..in`* em list comprehension nós podemos criar variáveis que podem ser usadas no output e em tudo que venha depois da definição de *`let..in`*.
```haskell
calcBMI :: [(Double, Double)] -> [Double]
calcBMI xs = [bmi | (weight, height) <- xs, let bmi = weight / height ^ 2]


calcBMI [(85, 1.81), (70, 1.9), (60, 1.5), (90, 1.8)]
[25.94548395958609,19.390581717451525,26.666666666666668,27.777777777777775]


getOverweight :: [(Double, Double)] -> [Double]
getOverweight xs = [bmi | (weight, height) <- xs, let bmi = weight / height ^ 2, bmi > 25.0]


getOverweight [(85, 1.81), (70, 1.9), (60, 1.5), (90, 1.8)]
[25.94548395958609,26.666666666666668,27.777777777777775]
```
Neste caso não necessitamos funções auxiliares para nossas list comprehension.

*`Haskell`* tem uma forma diferente para fazer *`Pattern Matching`* que é o *`case..of`*. Ambos fazem o mesmo, mas como uma expressão *`case..of`* pode ser usado em qualquer lugar e *`Pattern Matching`* não.
```haskell
head' :: [a] -> a
head' xs = case xs of
  [] -> error "empty list"
  (x:_) -> x


head' []
*** Exception: empty list


head' [1]
1


head' [1,2]
1


listType :: [a] -> String
listType xs = "This is " ++ case xs of
  [] -> "an empty list"
  [a] -> "list with a single element"
  _ -> "a list with more than one element"


listType []
"This is an empty list"


listType [1]
"This is list with a single element"


listType [1,2]
"This is a list with more than one element"
```
Com o *`case..of`* nós podemos criar uma função com *`Pattern Matching`* ou adiciona-la dentro de outras expressões.

<br />

Hoje vimos outras possibilidades para trabalhar com listas e às vezes não usar *`Pattern Matching`*. Com esse conteúdo nós finalizamos o terceiro capítulo do livro “Learn You a Haskell for Great Good!: A Beginner’s Guide”.
