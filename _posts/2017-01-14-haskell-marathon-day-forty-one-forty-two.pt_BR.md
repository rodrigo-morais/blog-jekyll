---
layout: post
title: Maratona de Haskell - Quadragésimo Primeiro à Quadragésimo Segundo Dia
published: true
lang: pt_BR
translation: true
---

Fala galera!

Nós terminamos nossos exercícios com a *`Binary Search Tree`* no último post e agora vamos voltar a seguir o [livro](http://learnyouahaskell.com/) que estavamos seguindo.  
Hoje vamos iniciar a falar sobre módulo em *`Haskell`*.

<br />

**O que são módulos?**

Bem, módulos são arquivos onde podemos defininir functions, types e type classes.  
Um módulo tem um monte de definições e podemos exportar apenas algumas delas. Essa é a mesma ideia que temos de público e privado em orientação a objeto.

<!--more-->

Separar o código em módulos é um bom sinal e nos da alguma vantagens. A primeira deve ser reusabilidade, se temos funções e tipos que podem ser chamados por outros módulos é uma boa ideia coloca-los por similariedade no mesmo módulo para deixar simples o seu reuso. Outo benefício seria a manutenabilidade porque se funções e tipos relacionados estão no mesmo módulo é mais fácil cuidar deles.

<br />

**Importando um módulo**

Vamos dizer que queremos usar uma determinada função de um determinado módulo como *`nub`* do módulo *`Data.List`*. A função *`nub`* remove valores duplicados da lista. Para usa-la temos que importar o módulo.  
Vamos ver como se importa o módulo:
```haskell
import Data.List
```
Com esta linha nós estamos importando todas as funções e tipos que o módulo *`Data.List`* exporta.  
Agora nós podemos usar a função *`nub`*.
```haskell
Data.List> nub [1,1,2,3,1,4,2,5,2,3,4,6]
[1,2,3,4,5,6]
```
E tudo funciona bem. Se não importamos o módulo recebemos um erro:
```haskell
> nub [1,1,2,3,1,4,2,5,2,3,4,6]
<interactive>:2:1: Not in scope: ‘nub’
```

<br />

**Importar somente algumas funções**

Quando usamos *`import`* como acima nós estamos importando todas as funções do módulo. Para importar somente as funções que necessitamos nós temos que dizer para o *`Haskell`* quais são as funções que queremos como isso:
```haskell
import Data.List (nub, sort)
```
Agora apenas importamos as funções *`nub`* e *`sort`* e todas as outras funções do módulo *`Data.List`*  não estão disponiveis para uso.

<br />

**Eliminando algumas funções**

Do mesma forma que podemos escolher as funções que queremos importar é possível fazer o oposto e escolher as que não queremos. Fazer isso é muito simples:
```haskell
import Data.List hiding (nub)

> nub [1,1,2,3,1,4,2,5,2,3,4,6]
<interactive>:2:1: Not in scope: ‘nub’
```
E agora temos todas as funções do módulo *`Data.List`* menos a função *`nub`*.

<br />

**Dando um alias para o módulo**

As vezes dois módulos possuem o mesmo nome de função ou o nosso projeto tem o mesmo nome de função que o módulo que estamos importando tem. Neste caso *`Haskell`* nos da a oportunidade de criar um alias para o módulo importado e assim continuar usando suas funções. 
```haskell
> import qualified Data.List as L

L> L.nub [1,1,2,3,1,4,2,5,2,3,4,6]
[1,2,3,4,5,6]
```
Agora nós podemos usar a letra *`L`* para acessar as funções do módulo.

<br />

Hoje vimos como importar módulos em *`Haskell`*.  
Próximos posts nós continuaremos vendo como módulos funcionam em *`Haskell`*.
