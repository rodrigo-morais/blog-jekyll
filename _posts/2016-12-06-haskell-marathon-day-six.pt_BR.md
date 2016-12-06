---
layout: post
title: Maratona de Haskell - Sexto Dia
published: true
lang: pt_BR
translation: true
---

Fala pessoal!


Ontem nós entendemos como tipos funcionam em *`Haskell`*, quais os tipos que *`Haskell`* suporta e que nós temos tipos variáveis que podem nos ajudar bastante.
Hoje vamos falar sobre *`type classes`*. Primeiro de tudo temos que dizer que *`type classes`* não são classes. Com este aviso nós podemos ir em frente e descobrir o que diabos são *`type classes`*.


<!--more-->

*`Type class`* não é mais que uma interface que descreve alguns comportamentos. Se um tipo é uma instância de uma *`type class`*, então ele implementa seus comportamentos.
Para ser mais claro, *`type class`* é somente uma coleção de funções que decidimos que fazem sentido para um tipo.
As mais comuns *`type classes`* em *`Haskell`* são *`Eq`*, *`Ord`*, *`Show`*, *`Read`*, *`Enum`*, *`Bounded`*, *`Num`*, *`Floating`* e *`Integral`*. Vamos dar uma rápida resumida neles.

<br />

**Eq type class**

Primeiro vamos validar o tipo do operador *`==`* que é uma instância de *`Eq`*.
```haskell
:t (==)
(==) :: Eq a => a -> a -> Bool
```
Como nós já sabemos o *`:t`* retorna o tipo de um valor ou função. O operador *`==`* é uma função e nós podemos ver seus tipos. Nós já aprendemos como le-los. A função recebe dois tipos variáveis chamados "a" e retorna um *`Bool`*. Mas espere um minuto, que diabos é *`Eq a =>`*? *`Eq a =>`* quer dizer que o tipo "a" deve ser uma instância da classe *`Eq`*.
As instâncias de *`Eq`* implementam duas funções que são *`==`* e *`/=`*.

<br />

**Ord type class**

*`Ord`* é um *`type class`* para tipos cujo os valores podem ser ordenados. Vamos dar uma olhada em um  operador para o *`type class`* *`Ord`*.
```haskell
:t (<)
(<) :: Ord a => a -> a -> Bool
5 < 6
True
5 < 4
False
```
O tipo *`<`* é similar a *`==`* qual nós vimos anteriormente. Todos os tipos que cobrimos anteriormente são instâncias de *`Ord`*, somente as funções não são. Os operadores de *`Ord`* são *`<`*, *`<=`*, *`>`* e *`>=`*.

<br />

**Show type class**

Tipos que são instâncias de do *`type class`* *`Show`* podem ser representados por strings. Como *`Ord`*, todos os tipos que foram cobertos são instâncias do *`type class`* *`Show`*, somente as funções que não. O comportamento do *`type class`* *`Show`* é printar valores.
```haskell
show 5
"5"
show 'a'
"'a'"
show True
"True"
```

<br />

**Read type class**

O comportamento do *`type class`* *`Read`* é o oposto do comportamento do *`type class`* *`Show`*, mas todo o resto é o mesmo. Ele lê uma string e transforma em valor.
```haskell
read "True" || False
True
read "True" && False
False
read "5" + 4
9
read "['a']" ++ ['h']
"ah"
```

<br />

**Enum type class**

O *`type class`* *`Enum`* tem o comportamento de montar sequências. Então toda as instâncias de *`Enum`* são tipos sequencialmente ordenados e valores podem ser enumerados. Essas instâncias podem ser usadas em intervalo de listas e possuem sucessor e predecessor.
```haskell
['a'..'f']
"Abcdef"
[3..9]
[3,4,5,6,7,8,9]
```

<br />

**Num type class**

*`Num`* é um *`type class`* numérico. Suas instâncias podem atuar como números.
```haskell
:t 5
5 :: Num a => a
5 :: Int
5
5 :: Integer
5
5 :: Float
5.0
5 :: Double
5.0
```

<br />

**Floating type class**

O *`type class`* *`Floating`* tem instâncias do tipo *`Float`* e *`Double`*. As funções que são instâncias do *`type class`* *`Floating`* devem representar pontos flutuantes.
```haskell
sin 2
0.9092974268256817
cos 2
-0.4161468365471424
```

<br />

**Integral type class**

O *`type class`* *`Integral`* é outro *`type class`* numérico que inclue *`Int`* e *`Integer`*.

<br />

Um tipo pode ser instância de multiplos *`type classes`*. Temos que pensar, que como uma interface, cada *`type class`* possue comportamentos que devem ser seguidos. Por exemplo, um tipo pode ser uma instância do *`type class`* *`Eq`*  e do *`type class`* *`Ord`* e ter igualdade e ordenação como comportamentos.  
Parece que *`type classes`* não são muito útils para nós agora, mas em itens mais complexos do *`Haskell`* esse conhecimento vai nos ajudar.
