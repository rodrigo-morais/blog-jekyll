---
layout: post
title: Haskell's Marathon - Day Five
title: Maratona de Haskell - Quinto Dia
published: true
lang: pt_BR
translation: true
---

Fala pessoal!


Qual é o seu tipo?  
Hoje nós vamos entender, ou tentar, um pouco como o sistemas de tipo de *`Haskell`* funciona.


Em *`Haskell`* tudo tem um tipo e eles são validados em tempo de compilação. Isso faz o código ser mais seguro, porque os erros são pegos brevemente e não durante a execução.  
Diferentemente de outras linguagens como *`Java`* e *`C#`*, *`Haskell`* tem inferência de tipos. Isso significa que não é necessário dizer para o *`Haskell`* qual o tipo de cada elemento, e nosso código não se torna verboso.

<!--more-->

Se *`Haskell`* é uma linguagem estaticamente tipada nós temos que ter uma forma de obter os tipos de funções e valores. Para isso que podemos usar *`:t`* que nós da o tipo de valores e funções. Vamos ver:


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
O operador *`::`* é chamado “has type of” e o tipo explícito são sempre denotados com a primeira letra em maíusculo.
Um importante item é a função que vimos acima. Ela retorna um tipo diferente. O tipo da função significa que a funão *`fnt`* irá receber um tipo *`t`* e retornar um tipo *`t`* onde *`t`* pode ser qualquer tipo válido em *`Haskell`*.


Mas o que são tipos válidos em *`Haskell`*?  
Podemos iniciar dizendo que *`Haskell`* tem dois tipos para inteiros que são o *`Int`* e o *`Integer`*. A diferença é que o tipo *`Integer`* é usado para números grandes.


```haskell
factorial :: Int -> Int
factorial n = product [1..n]


factorial' :: Integer -> Integer
factorial' n = product [1..n]


factorial 25
7034535277573963776


factorial’ 25
15511210043330985984000000
```

Para ponto flutuante *`Haskell`* tem dois tipos. *`Float`* é para precisção simples e *`Double`* para precisão dupla. *`Char`* e *`Bool`* são tipos também. E *`Tuple`* que vimos anteriormente são tipos também, elas dependem do tamanho e do tipo de seus componentes.

*`Haskell`* tem algo chamado tipos variáveis que é relacionado com o exemplo de função que vimos acima. Às vezes funções não tem um tipo definido e nós usamos os tipos variáveis para isso. Tipo variável em *`Haskell`* pode ser uma palavra, mas geralmente são usados um caracter como 'a' ou 'b'. Vamos dar uma olhada na função *`head`* que obtém o primeiro elemento de uma lista.
```haskell
head [1,2,3,4]
1
head [‘h’,’e’,’l’,’l’,’o’]
‘h’
:t head
head :: [a] -> a
```
Como nós vimos o tipo da função *`head`* é uma lista de qualquer tipo que retorna um elemento do mesmo tipo da lista.
Tipos variáveis são muito legais porque nos dão alguma liberdade quando não queremos criar regras severas para as funções ou quando a função pode trabalhar com diferentes tipos. Esse comporatmento é como *`generics`* em outras linguagens.


Hoje nós entendemos um pouco como *`Haskell`* trabalha com tipos. Amanhã vamos ver *`type classes`* e que elas não são classes.
