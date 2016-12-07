---
layout: post
title: Maratona de Haskell - Sétimo Dia
published: true
lang: pt_BR
translation: true
---

Fala pessoal!


Hoje o estudo sobre *`Haskell`* foi um pouco diferente. Ao invés de seguir o livro eu fui a um meetup. Este foi meu primeiro meetup em Berlim e fui muito legal e diferente.  
Este meetup acontece todas as Quarta-feiras e cada semana tem um diferente objetivo. Uma semana é um meetup com palestras e etc, e na outra é para iniciantes aprenderem a linguagem.  
Hoje o meetup foi para iniciantes. O grupo esta seguindo um livro chamado [“Haskell Programming”](http://haskellbook.com/) e hoje eles cobriram o oitavo capítulo que é sobre *`foldr`* e *`foldl`*.

<!--more-->

O meetup inicíou com uma revisão sobre o capítulo sete que foi sobre Lists e funções como *`map`*, *`filter`* e *`zip`*. A parte legal foi que discutimos como implementar essas funções manualmente. Isso foi interessante porque os participantes puderam compartilhar ideias e experiências e assim contruimos a solução juntos. E além disso nos tornamos mais concientes de como as funções funcionam e mais seguro de usa-las.

Depois disso nós falamos sobre as funções *`foldr`* e *`foldl`* que são uteis para se trabalhar com listas. Elas funcionam como *`reduce`* em outras linguagens.
```haskell
foldr (+) 0 [1..10]
55
foldl (+) 0 [1..10]
55
```
A diferença é que uma inicia da esquerda e outra da direita. Vamos falar sobre essas funções e  *`map`*, *`filter`*, *`zip`* e etc em breve.

<br />

Se você vier ou esta em Berlim eu realmente recomendo este [meetup](https://www.meetup.com/berlinhug/). Pessoas inteligentes e prestativas com diferentes backgrounds e níveis de conhecimento sobre *`Haskell`*.
