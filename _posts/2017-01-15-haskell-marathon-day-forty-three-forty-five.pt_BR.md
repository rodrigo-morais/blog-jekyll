---
layout: post
title: Maratona de Haskell - Quadragésimo Terceiro à Quadragésimo Quinto
published: true
lang: pt_BR
translation: true
---

Fala galera!

No último post nós vimos como importar módulos e agora vamos ver como criar nossos próprios módulos.  

Como vimos no último pos criar um módulo para colocar funções e tipos que devem trabalhar juntos é uma boa prática.

<br />

**Criar um módulo**

Criar um novo módulo é super simples e somente temos que colocar essa linha de código no topo do arquivo.
<!--more-->
```haskell
module BST where
```
Essa é a sintaxe, nós usamos a palavra *`module`*, o nome módulo que desejamos e a palavra *`where`*.  
Nesse exemplo nós criamos um módulo para a *`BST`* que trabalhamos alguns posts atrás.

<br />

**Usando o módulo**

Para usar o módulo nesse caso é um pouco diferente porque temos que carregar o arquivo. Geralmente os módulos são instalados em *`Haskell`* quando instalamos uma nova biblioteca então apenas importamos eles. No nosso caso estamos trabalhando com um módulo local então temos que carrega-lo primeiro.
```haskell
Prelude> :l code/binary-tree.hs

code/binary-tree.hs:1:14: Warning:
    -XDatatypeContexts is deprecated: It was widely considered a misfeature, and has been removed from the Haskell language.
[1 of 1] Compiling BST              ( code/binary-tree.hs, interpreted )
Ok, modules loaded: BST.

*BST> :m

Prelude> import BST

Prelude BST> BST.build [5,4,6,8,3,2,9]
Node 5 (Node 4 (Node 3 (Node 2 Empty Empty) Empty) Empty) (Node 6 Empty (Node 8 Empty (Node 9 Empty Empty)))
Prelude BST>
```
Primeiro carregamos o arquivo usando o comando *`:l`* e o nome do arquivo. Nesse momento o módulo deste arquivo é carregado. Somente para confirmar podemos notar que a command line mudou o texto *`Prelude`* para *`BST`*.  
Segundo passo é para remover o módulo com o comando *`:m`*.  
No último passo importamos nosso módulo como nós vimos no último post e podemos usar suas funções.

<br />

**Selecionando as funções públicas**

No exemplo acima todas as funções do módulo estão disponíveis. Nós podemos mudar isso e somente exportar as funções que queremos que sejam públicas. Se tentarmos usar a função *`build'`* com a abordagem acima nós podemos.
```haskell
Prelude BST> BST.build' [5,4,6,8,3,2,9] Empty
Node 5 (Node 4 (Node 3 (Node 2 Empty Empty) Empty) Empty) (Node 6 Empty (Node 8 Empty (Node 9 Empty Empty)))
```

Agora vamos dizer para nosso módulo quais funções devem ser públicas:
```haskell
module BST
( build
, build2
, build3
, insert
, find
, findSub
, contains
, size
, height
, delete
) where
```
Com isso dizemos para o *`Haskell`* quais são as funções que devem ser públicas.  

Se importarmos e tentarmos usar a função *`build'`* de novo nós receberemos um erro:
```haskell
Prelude> :l code/binary-tree.hs

code/binary-tree.hs:1:14: Warning:
    -XDatatypeContexts is deprecated: It was widely considered a misfeature, and has been removed from the Haskell language.
[1 of 1] Compiling BST              ( code/binary-tree.hs, interpreted )
Ok, modules loaded: BST.

*BST> :m

Prelude> import BST

Prelude BST> BST.build' [5,4,6,8,3,2,9] Empty

<interactive>:26:1:
    Not in scope: ‘BST.build'’
    Perhaps you meant one of these:
      ‘BST.build’ (imported from BST), ‘BST.build2’ (imported from BST),
      ‘BST.build3’ (imported from BST)

<interactive>:26:28: Not in scope: data constructor ‘Empty’

Prelude BST> BST.build [5,4,6,8,3,2,9]
Node 5 (Node 4 (Node 3 (Node 2 Empty Empty) Empty) Empty) (Node 6 Empty (Node 8 Empty (Node 9 Empty Empty)))
```
Mas a função *`build`* esta disponível para nós porque dissemos que ela era pública.

<br />

A *`BST`* com módulo esta em meu [GitHub](https://github.com/rodrigo-morais/haskell-exercises/blob/master/binary-tree.hs).  
Agora já sabemos como criar e importar um módulo em *`Haskell`*.
