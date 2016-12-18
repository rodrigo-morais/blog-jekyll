---
layout: post
title: Maratona de Haskell - Décimo Sétimo e Oitavo Dias
published: true
lang: pt_BR
translation: true
---

Fala pessoal!

Estes útlimos dias eu estudei sobre *`folds`* e *`scan`*.
 
Então hoje vamos começar falando sobre *`folds`* que são o mesmo que *`reducers`* em outras linguagens. *`Haskell`* tem dois tipos de *`folds`* que são *`foldl`* e *`foldr`*.

<!--more-->

### foldl

A função *`foldl`* é usada quando queremos executar a lista da esquerda para a direita. Por exemplo se temos uma lista [1,2,3,4,5] com *`foldl`* nós vamos fazer esse processo:
(((((0 + 1) + 2) + 3) + 4) + 5) => ((((1 + 2) + 3) + 4) + 5) => (((3 + 3) + 4) + 5) => ((6 + 4) + 5) => (10 + 5) => 15

A função *`foldl`* tem essa assinatura *`foldl :: (b -> a -> b) -> b -> [a] -> b`* que esta dizendo que receberemos uma função, um elemento de qualquer tipo, uma lista e retornaremos um elemento como resultado.  
A função será aplicada sobre a lista e o segundo elemento é um acumulador.  
Vamos ver como isso funciona:
```haskell
foldl (+) 0 [1,2,3,4,5]
15

foldl (*) 3 [1,2,3,4,5]
360
```
Então no primeiro exemplo que a função recebida foi *`(*)`*, o acumulador foi *`0`* e a lista recebida foi *`[1,2,3,4,5]`*. O resultado foi *`15`* como haviamos simulado anteriormente.

Eu reescrevi a função *`foldl`*. Vamos ver como ficou:
```haskell
foldl' :: (b -> a -> b) -> b -> [a] -> b
foldl' _ acc [] = acc
foldl' f acc (x:xs) = foldl' f (f acc x) xs

foldl' (+) 0 [1,2,3,4,5]
15

foldl' (*) 3 [1,2,3,4,5]
360
```

<br />

### foldr

A função *`foldr`* é similar a função a função *`foldl`* mas a computação é feita da direita para a esquerda. Vamos ver um exemplo com a soma de uma lista [1,2,3,4,5]:  
(1 + (2 + (3 + ( 4 + (5 + 0))))) => (1 + (2 + (3 + ( 4 + 5)))) => (1 + (2 + (3 + 9))) => (1 + (2 + 12)) => (1 + 14) => 15

A assinatura da função *`foldr`* é *`foldr :: (a -> b -> b) -> b -> [a] -> b`*.  
Vamos ver alguns exemplos:
```haskell
foldr (+) 0 [1,2,3,4,5]
15

foldr (*) 3 [1,2,3,4,5]
360
```
Somente o mesmo que *`foldl`*.  
A função *`foldr`* brilha quando usada para concatenar listas ou com listas infinitas. Com a concatenação de listas porque o operador *`:`* é muito mais barato do que o *`++`* para concatenar listas, e a maioria do tempo usamos *`foldr`* e *`:`* ou *`foldl`* e *`++`*. Sobre listas infinitas porque em algumas listas *`foldl`* não funciona enquanto *`foldr`* continua funcionando. Isso acontece porque *`foldr`* não necessita de toda lista para avaliar a função tomando vantagem do laziness do *`Haskell`*.  
Abaixo o código para reescrever a função *`foldr`*.
```haskell
foldr'' :: (a -> b -> b) -> b -> [a] -> b
foldr'' _ acc [] = acc
foldr'' f acc (x:xs) =
  f x (foldr'' f acc xs)
```

Para ver a diferenção entre *`foldl`* e *`foldr`* nós temos que usar funções com divisão ou subtração. Vamos ver isso:
```haskell
foldl (-) 100 [54,20]
26

foldr (-) 100 [54,20]
134
```
Aui o *`foldl`* computa os valores nessa ordem *`((100 - 54) - 20)`* e *`foldr`* nessa ordem *`(54 - (20 - 100))`* e por causa disso os resultados são diferentes.  
Outro exemplo com divisão:
```haskell
foldl (/) 100 [5,2]
10.0

foldr (/) 100 [5,2]
250.0
```
A mesma ideia que vimos antes.

<br />

### Scan

Agora vamos dar uma rápida olhada em outra função chamada *`scan`*. Essa função faz o mesmo que *`fold`* mas o resultado não é somente um valor, mas sim uma lista. A lista tem todos os acumuladores criados durante a computação. *`Scan`* tem duas funções como *`fold`* que são *`scanl`* e *`scanr`*.  
Vamos comparar *`scan`* e *`fold`*:
```haskell
foldl (/) 100 [5,2]
10.0

scanl (/) 100 [5,2]
[100.0,20.0,10.0]

foldr (/) 100 [5,2]
250.0

scanr (/) 100 [5,2]
[250.0,2.0e-2,100.0]
```

Pode ver? Nós temos o resulatdo final, mas *`scan`* trouxe todos os acumuladores que foram computados. Na função *`scanl`* nós temos o resultado no final da lista e em *`scanr`* no início.
