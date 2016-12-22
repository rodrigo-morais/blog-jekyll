---
layout: post
title: Haskell's Marathon - Days Nineteen to Twenty Two
title: Maratona de Haskell - Décimo Nono até Vigésimo Segundo Dia
published: true
lang: pt_BR
translation: true
---

Fala pessoal!

Vamos começar falando sobre o operador *`Functional Application`* que è uma função que nos ajuda a remover os parênteses de nossas funções. Enquanto *`Function Application`* com espaços são associadas à esquerda a *`Function Application`* com *`$`* é associada à direita e por causa disso nós podemos adicionar funções sem parênteses.

Function Application com espaços: f a b c => ((f a) b) c)  
Function Application com $: f a b c => (f (a (b c)))

<!--more-->

Vamos ver alguns exemplos com o operador *`Function Application`*:
```haskell
sqrt 3 + 2 * 5
1.732050807568877

sqrt (3 + 2 * 5)
3.605551275463989

sqrt $ 3 + 2 * 5
3.605551275463989
```
Nós podemos ver aqui que *`$`* nos permite remover os parênteses.

Outro exemplo:
```haskell
foldl (+) 0 (tail (map (*2) [1,2,3,4,5,6,7]))
54

foldl (+) 0 $ tail $ map (*2) [1,2,3,4,5,6,7]
54
```
No segundo exemplo nós podemos remover todos os parênteses.

<br />

Agora vamos dar uma olhada em *`Function Composition`* que é a forma que podemos compor funções. *`Function Composition`* é representada em *`Haskell`* por um *`.`* (ponto). As vezes *`Function Composition`* nos permite remover alguns parênteses como *`Function Application`*, mas sua principal responsabilidade é compor funções.
```haskell
map (\x -> negate (abs x)) [1,-2,3,-4,5,-6,7]
[-1,-2,-3,-4,-5,-6,-7]

map (negate .abs) [1,-2,3,-4,5,-6,7]
[-1,-2,-3,-4,-5,-6,-7]
```
Veja que removemos a função anônima somente deixando as funções e removemos os parênteses. Isso acontece porque *`Function Composition`* somente functiona com funções que esperam um parâmetro.

```haskell
sumTail :: (Num a, Ord a) => [a] -> [a] -> a
sumTail xs ys = foldl (+) 0 . tail . map (negate . abs) $ zipWith max xs ys

sumTail [1,2,3] [4,5,6]
-11
```
E nós posdemos combinar *`Function Application`* com *`Function Composition`* e obter funções mais limpas e legíveis.
