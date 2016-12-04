---
layout: post
title: Maratona de Haskell - Primeiro Dia
published: true
lang: pt_BR
translation: true
---

Hoje foi o primeiro dia da minha maratona de *`Haskell`* e eu gostaria de compartilhar com vocês meus aprendizados e entendimentos.

<br />

**Configuração**

Vamos iniciar com como configurar seu computador para usar *`Haskell`*. Você tem que instalar o *`Haskell`* compilador que é chamado *`GHC`*. Os passo de instalação estão nesse [link](https://www.haskell.org/platform/).
Minha dica é não instalar o compilador do *`Haskell`* em sua máquina, e sim usar uma imagem *`Docker`* com *`Haskell`* para isso. Se você não tem *`Docker`* instalado em seu computador você pode ver como instala-lo [aqui](https://www.docker.com/products/overview). Depois de instalar o *`Docker`* você somente necessita inicia-lo e rodar o comando: **docker run -ti --rm -v $(pwd):/code haskell:7.10 bash**. Agora você tem uma máquina virtual rodando o compilador do *`Haskell`* para você. Para iniciar o interpretador do *`GHC`*  você tem que executar o comando: **ghci**.

<!--more-->

<br />

**Imutabilidade**

*`Haskell`*, como uma linguagem de funcional pura, trabalha com imutabilidade. Isso significa que você não tem variaveis e quando um valor é setado para uma container de dados é impossível muda-lo. *`Haskell`* não possue side effects e isso nos da mais segurança que sempre que chamamos uma função com um valor o resultado será o mesmo. Essa característica aumenta a testabilidade do *`Haskell`* e nós não temos que procurar onde a variavél foi modificada e porque esta afetando os funcionamento de uma função.

<br />

**Lazy**

*`Haskell`* é *`lazy`*. Isso significa que *`Haskell`* somente faz a computação que é necessária e espera até o último momento para executar as funções e retornar os resultados.
Por exemplo, vamos dizer que temos uma lista com 1000 números que queremos converter em uma lista de módulos e obter o primeiro valor, para fazer isso *`Haskell`* irá processar a lista de módulo até encontrar o primeiro valor e irá parar.
```haskell
let xs = [1..999999]
xs
map (\x -> x `mod` 2) xs
head (map (\x -> x `mod` 2) xs)
```
Com esse exemplo você pode ver como *`Haskell`* é poderoso usando a sua demora de processamento. Quando nós rodamos as linhas 2 e 3 nós temos que esperar alguns segundos para obter o resultado, por outro lado quando executamos a linha 4 o resultado é retornado automáticamente. Isoo acontece porque *`Haskell`* para de processar assim que descobre o resultado.

<br />

**Tipo estático**

*`Haskell`* é estaticamente tipado, mas diferentemente de linguagens como *`Java`* or *`C#`* nós não temos que assinar tipos para tudo. *`Haskell`* infere os tipos para valores e funções e usa o compilador para avaliar os erros. Por isso *`Haskell`* não é considerada uma linguagem verbosa.

<br />

**Aritmética**

Os cálculos e processamentos aritméticos em *`Haskell`* são similares as outras linguagens de programação. Os precedentes universais da matématica são seguidos e respeitados.

<br />

**Boolean**

Booleanos em *`Haskell`* são similares as outras linguagens também. Temos os valores *`True`* e *`False`* e os operadores *`&&`* (e), *`||`* (ou) and *`not`* (negação). Para testar dois valores nós temos os operadores *`==`* (igual) e *`/=`* (diferente). Teste eles no *`GHCI`*.

<br />

**Funções**

Tudo em *`Haskell`* são funções ou quase tudo. Nós podemos não ter percebido mas *`+`* e *`-`* são funções. Esses tipos de funções são chamadas *`infix`* porque elas são chamadas entre os operandos como *`5 + 6`*. A maioria das funções são chamadas *`prefix`*, que são funções chamadas antes dos operandos como *`succ 9`*. Funções *`prefix`* podem ser chamadas como funções *`infix`*, para fazermos isso temos que coloca-las entre crases (\`) como em 9 \`div\` 3. O oposto também é possível, neste caso nós temos que colocar a função entre parênteses (()).  
Para criamos uma função nós temos que da-la um nome e parâmetros. Quando criamos uma função no *`GHCI`* é necessário usar *`let`*, mas se criamos uma função em um arquivo que será compilado não devemos usar o *`let`*.
Vamos criar algumas funções?
```haskell
Let mult2 x = x * 2
mult2 3
6
mult2 4
8
let add x y = x + y
add 2 3
5
add 3 3
6
```

<br />

Esses foram os meus primeiros passos com *`Haskell`*.
