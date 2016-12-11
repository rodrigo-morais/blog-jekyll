---
layout: post
title: Maratona de Haskell - Décimo Primeiro Dia - Parte 2
published: true
lang: pt_BR
translation: true
---

Fala pessoal!


Depois da revisão que fizemos anteriormente eu acho que é uma boa idea praticar com alguns exercícios. Eu trabalhei na lista chamada [99 questions](https://wiki.haskell.org/99_questions/1_to_10).
Resolvi os dez primeiros exercícios, vamos dar uma olhada em alguns deles:

<!--more-->
<br />

**Exercício Dois**


A descrição do exercício é: Find the last but one element of a list.

E este o exemplo:
```haskell
myButLast [1,2,3,4]
3

myButLast ['a'..'z']
'y'
```
Ok, como vimos no terceiro dia nós temos a função *`last`* para obter o último elemento de uma lista, mas aqui queremos o penúltimo elemento.
Se temos uma lista como [1,2,3,4,5] nós queremos retornar o número 4. Para fazer isso temos algumas funções para nos ajudar, uma é a função *`reverse`* que reverte a ordem de uma lista. A outra é a função *`!!`* que retorna o elemento do index informado. Lembre que *`Haskell`* inicia a lista com o index 0.
Se revertermos e obtermos o index 1 isso funcionará.
```haskell
myButLast :: [a] -> a
myButLast xs = reverse xs !! 1


myButLast [1,2,3,4]
3

myButLast ['a'..'z']
'y'
```

<br />

**Exercício Seis**



A descrição do exercício é: Find out whether a list is a palindrome. A palindrome can be read forward or backward; e.g. (x a m a x).

E este o exemplo:
```haskell
isPalindrome [1,2,3]
False


isPalindrome "madamimadam"
True


isPalindrome [1,2,4,8,16,8,4,2,1]
True
```
Este tem uma simples solução, mas é um famoso desafio inclusive em entrevistas de emprego.
Nós somente necessitamos comparar a lista recebida com a mesma revertida.
```haskell
isPalindrome :: (Eq a) => [a] -> Bool
isPalindrome xs = xs == reverse xs


isPalindrome [1,2,3]
False


isPalindrome "madamimadam"
True


isPalindrome [1,2,4,8,16,8,4,2,1]
True
```
Temos que prestar atenção que esta função implementa a *`type classes`* de igualdade.

<br />

**Exercício Oito**

A descrição do exercício é: Eliminate consecutive duplicates of list elements.
If a list contains repeated elements they should be replaced with a single copy of the element. The order of the elements should not be changed.

E este o exemplo:
```haskell
compress "aaaabccaadeeee"
"abcade"
```
Eu inicie usando uma função auxiliar que funcionou:
```haskell
compress :: (Eq a) => [a] -> [a]
compress [] = []
compress (x:[]) = [x]
compress (x:xs) = x : (compress $ (cleanRepeated x xs))


cleanRepeated :: (Eq a) => a -> [a] -> [a]
cleanRepeated _ [] = []
cleanRepeated x (y:ys) = if x == y then cleanRepeated x ys else y : ys


compress "aaaabccaadeeee"
"abcade"
```


Mas a solução não estava boa o suficiente. Então combinando *`Guards`* e *`as-pattern`* a função tornou-se mais simples:
```haskell
compress' :: (Eq a) => [a] -> [a]
compress' (x:xs@(y:_))
  | x == y = compress xs
  | otherwise = x : compress xs


compress "aaaabccaadeeee"
"abcade"
```

<br />

**Exercício Nove**


A descrição do exercício é: Pack consecutive duplicates of list elements into sublists. If a list contains repeated elements they should be placed in separate sublists.

E o exemplo:
```haskell
pack ['a', 'a', 'a', 'a', 'b', 'c', 'c', 'a',  'a', 'd', 'e', 'e', 'e', 'e']
["aaaa","b","cc","aa","d","eeee"]
```
Nós já vimos as funções *`take`* e *`drop`* que recebem um número de elementos para pega-los ou apaga-los. Eles tem irmãos que são chamados *`takeWhile`* e *`dropWhile`* que recebem uma função ao invés de um número.
```haskell
take 5 ['a', 'a', 'a', 'a', 'b', 'c', 'c', 'a',  'a', 'd', 'e', 'e', 'e', 'e']
"aaaab"


drop 5 ['a', 'a', 'a', 'a', 'b', 'c', 'c', 'a',  'a', 'd', 'e', 'e', 'e', 'e']
"ccaadeeee"


takeWhile (=='a') ['a', 'a', 'a', 'a', 'b', 'c', 'c', 'a',  'a', 'd', 'e', 'e', 'e', 'e']
"aaaa"


dropWhile (=='a') ['a', 'a', 'a', 'a', 'b', 'c', 'c', 'a',  'a', 'd', 'e', 'e', 'e', 'e']
"bccaadeeee"
```
Com essas funções é fácil resolver o problema:
```haskell
pack :: (Eq a) => [a] -> [[a]]
pack [] = []
pack (x:xs) = (x: takeWhile (==x) xs) : (pack $ dropWhile (==x) xs)


pack ['a', 'a', 'a', 'a', 'b', 'c', 'c', 'a',  'a', 'd', 'e', 'e', 'e', 'e']
["aaaa","b","cc","aa","d","eeee"]
```

<br />
<br />

Estes são alguns exercício que eu suponho foram mais difíceis de resolver considerando o nosso conhecimento de *`Haskell`*. Nos próximos dias eu trabalharei em mais exercícios.
