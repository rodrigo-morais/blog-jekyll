---
layout: post
title: Maratona de Haskell - Quarto Dia
published: true
lang: pt_BR
translation: true
---

Fala pessoal!


Hoje vamos falar um pouco mais sobre listas, mas nós vamos dar uma olhada também em tuplas.

<br />

**List Comprehension**

Nos dias dois e três nós vimos como criar e usar listas, hoje vamos continuar falando de outra forma de usar listas chamado list comprehension.
List comprehensions são o caminho para transformar, combinar e filtrar listas. Isso é similar ao conceito de set comprehension na matemática, mas nós não prestaremos atenção nisso.
Vamos iniciar dizendo que queremos gerar uma lista com os valores de 1 até 10 todos multiplicados por 2. Com list comprehension nós podemos fazer desta forma:
<!--more-->
```haskell
[ x*2 | x <- [1..10]]
[2,4,6,8,10,12,14,16,18,20]
```

Muito fácil. Vamos fazer isso um pouco mais complexo e dizer que somente queremos os valores maior que 10:
```haskell
[ x*2 | x <- [1..10], x*2 > 10]
[12,14,16,18,20]
```

Outra coisa que podemos fazer com list comprehension além de transformar e filtrar é combinação. Vamos combinar três listas:
```haskell
[x+y+z | x <- [1,2,3], y <- [101,102,103], z <- [1001,1002,1003]]
[1103,1104,1105,1104,1105,1106,1105,1106,1107,1104,1105,1106,1105,1106,1107,1106,1107,1108,1105,1106,1107,1106,1107,1108,1107,1108,1109]
```

Agora vamos tentar o list comprehension com uma lista de listas e somente pegar os números ímpares:
```haskell
let a = [1,2,3,4,5]
let b = [7,8,9,2,3,4,5]
let c = [11,12,13,14,15,16,17,18]
[ [ x | x <- xs, odd x ] | xs <- [a,b,c] ]
[[1,3,5],[7,9,3,5],[11,13,15,17]]
```

O list comprehension é realmente uma poderosa feature do *`Haskell`*, e nós ainda trabalharemos com isso hoje.

<br />

**Tuplas**

Tuplas são usados em *`Haskell`* para armazenar tipos heterogênios. Existem algumas similariedades entre listas e tuplas, mas além de tuplas serem heterogêneas elas tem tamanho fixo também.
```haskell
(1,2)
(1,2)
(1,2,”hello”)
(1,2,”hello”)
(1,2,”hello”, True)
(1,2,”hello”, True)
```

Tuplas tem tamanho fixo então nós só devemos usa-las quando sabemos quantos elementos vamos necessitar.
Quando tuplas tem dois elementos nós podesmos usar as funções *`fst`* e *`snd`*.
```haskell
fst (2,5)
2
snd (2,5)
5
```

Nós podemos usar o list comprehension que vimos antes combinado com tuplas e obter todas a combinações de listas. Vamos tentar:
```haskell
[(x,y,z) | x <- [1,2,3], y <- [101,102,103], z <- [1001,1002,1003]]
[(1,101,1001),(1,101,1002),(1,101,1003),(1,102,1001),(1,102,1002),(1,102,1003),(1,103,1001),(1,103,1002),(1,103,1003),(2,101,1001),(2,101,1002),(2,101,1003),(2,102,1001),(2,102,1002),(2,102,1003),(2,103,1001),(2,103,1002),(2,103,1003),(3,101,1001),(3,101,1002),(3,101,1003),(3,102,1001),(3,102,1002),(3,102,1003),(3,103,1001),(3,103,1002),(3,103,1003)]
```

Aqui cada tupla é uma combinação.

<br />

Amanhã nós iremos iniciar a mergulhar nos tipos de *`Haskell`*.
