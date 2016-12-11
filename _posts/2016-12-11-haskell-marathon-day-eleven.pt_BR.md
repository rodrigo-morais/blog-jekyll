---
layout: post
title: Maratona de Haskell - Décimo Primeiro Dia - Parte 1
published: true
lang: pt_BR
translation: true
---

Fala Pessoal!


Ontem nós finalizamos os três primeiros capítulos do [livro](http://learnyouahaskell.com/) que estamos acompanhando. Hoje vamos dividir nosso dia em duas partes. Primeiro vamos fazer uma revisão dos 10 primeiros dias e depois alguns exercícios.


Primeiro vamos para uma rápida revisão.
<!--more-->

<br />

**Primeiro Dia**

O [primeiro dia](https://rodrigo-morais.github.io/haskell-marathon-day-one/) foi uma básica introdução para o *`Haskell`* e como configurar nosso ambiente. Eu acho que o mais importante foi a dica de usar *`Docker`* porque isso torna tudo mais fácil.
Então instale *`Docker`*, rode o comando docker run -ti --rm -v $(pwd):/code haskell:7.10 bash e aproveite o *`Haskell`*.

<br />

**Segundo Dia**

O [segundo dia](https://rodrigo-morais.github.io/haskell-marathon-day-two/) nós trouxemos um dos mais importantes conceitos em *`Haskell`* que é *`List`* e além disso falamos sobre *`IF`* que é simples e um conceito universal no mundo do desenvolvimento de software.
Vamos ver alguns exemplos de listas:
```haskell
let numbers = [1,2,3,4]
numbers
[1,2,3,4]
let words = [“car”,”ball”,”gremio”]
words
[“car”, “ball”, “gremio”]
```
E algo sobre *`IF`* também.

<br />

**Terceiro Dia**

No [terceiro dia](https://rodrigo-morais.github.io/haskell-marathon-day-three/) nós mergulhamos mais no assunto das listas.
Aprendemos sobre listas aninhadas, comparação de listas e intervalo de listas:
```haskell
-- Nested lists
[[1,2,3],[4,5,6]]
[[1,2,3],[4,5,6]]


[['h','e','l','l','o'],['w','o','r','l','d']]
["hello","world"]


-- Comparing lists
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


-- Range of lists
[1..20]
[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]


['A'..'s']
"ABCDEFGHIJKLMNOPQRSTUVWXYZ[\\]^_`abcdefghijklmnopqrs"
```
Nós também estudamos sobre outros operadores.

<br />

**Quarto Dia**


Durante o [quarto dia](https://rodrigo-morais.github.io/haskell-marathon-day-four/) nós continuamos falando de lista e vimos algum conteúdo sobre *`Tuples`*.
Primeiro uma rápida revisada em um assunto realmente importante que é *`list comprehension`*.
```haskell
[ x*2 | x <- [1..10], x*2 > 10]
[12,14,16,18,20]
```
Depois uma olhada em como usar *`Tuples`* em *`Haskell`*.
```haskel
(1,2)
(1,2)
(1,2,”hello”)
(1,2,”hello”)
(1,2,”hello”, True)
(1,2,”hello”, True)
```
<br />

**Quinto Dia**


No [quinto dia](https://rodrigo-morais.github.io/haskell-marathon-day-five/) nós estudamos o que são *`static types`* em *`Haskell`* e os tipos válidos que são *`Int`*, *`Integer`*, *`Float`*, *`Double`*, *`Bool`*, *`Char`* e *`Tuples`*.
Nós também vimos como descrobrir os tipos de expressões, valores e funções usando *`:t`*:
```haskell
:t ‘a’
‘a’ :: Char
:t True
True :: Bool
:t 5
5 :: Num a => a
let fnt x = x
fnt 4
4
fnt ‘a’
‘a’
:t fnt
fnt :: t -> t
```

<br />

**Sexto Dia**


O [sexto dia](https://rodrigo-morais.github.io/haskell-marathon-day-six/) foi sobre *`type classes`* e que elas não são classes. Nós vimos as mais importantes *`type classes`* em *`Haskell`*.

<br />

**Sétimo Dia**


O [sétimo dia](https://rodrigo-morais.github.io/haskell-marathon-day-seven/) foi um dia diferente. Eu fui em um meetup de *`Haskell`* onde o grupo esta seguindo este [livro](http://haskellbook.com/) e nós trabalhamos com *`folds`*.

<br />

**Oitavo Dia**


O [oitavo dia](https://rodrigo-morais.github.io/haskell-marathon-day-eight/) foi um dia realmente  importante porque nós estudamos *`Pattern Matching`* . Este assunto é realmente importante e deve ser revisado. Aqui um exemplo:
```haskell
month' :: Int -> String
month' 5 = "May"
month' 6 = "June"
month' 7 = "July"
month' 8 = "August"
month' _ = "it is not a valid month"


month 5
"May"


month 6
"June"


month 7
"July"


month 9
"it is not a valid month"
```

<br />

**Nono Dia**


No [nono dia](https://rodrigo-morais.github.io/haskell-marathon-day-nine/) nós vimos algumas outras opções para *`Pattern Matching`* como *`Guards`* e *`where`*.
```haskell
bmiStatus' :: Double -> Double -> String
bmiStatus' weight height
  | bmi <= 18.5 = "You are underweight!"
  | bmi <= 25 = "You are with ideal weight!"
  | bmi <= 30 = "You are overweight!"
  | otherwise = "You are obese!"
  where bmi = weight / height ^ 2


bmiStatus’ 85 1.81
"You are overweight!"


bmiStatus’ 80 1.81
"You are with ideal weight!"


bmiStatus’ 60 1.81
"You are underweight!"


bmiStatus’ 100 1.81
"You are obese!"
```

<br />

**Décimo Dia**


No [último dia](https://rodrigo-morais.github.io/haskell-marathon-day-ten/) nós vimos mais opções para *`Pattern Matching`* como *`let..in`* and *`case..of`*:
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
```
