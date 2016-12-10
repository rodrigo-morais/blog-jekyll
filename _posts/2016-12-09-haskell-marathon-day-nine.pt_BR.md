---
layout: post
title: Maratona de Haskell - Nono Dia
published: true
lang: pt_BR
translation: true
---

Fala pessoal!

Ontem nós falamos sobre *´Pattern Matching`* e hoje nós vamos iniciar com um especial caso de *`Pattern Matching`*. Se nós precisamos da lista original durante o *`Pattern Matching`* nós podemos usar algo chamado *`as-pattern`*. Eu não acho este caso especial tão útil, mas eu vou mostrar um exemplo:
<!--more-->
```haskell
firstLetter :: String -> String
firstLetter all@(x:xs) = "The first letter of " ++ all ++ " is " ++ [x]


firstLetter "Haskell"
"The first letter of Haskell is H"
```


Agora vamos falar sobre algo importante. *`Guards`* são outra forma de fazer *`Pattern Matching`* onde podemos comparar valores. Ele é mais similar ao *`IF/ELSE`* que *`Pattern Matching`* é. Quando recebemos um valor é possível validar se alguma propriedade é verdadeira ou falsa o qual não pode ser feito com *`Pattern Matching`*, mas nós podemos fazer com *`Guards`*. Vamos ver um exemplo:
```haskell
bmiStatus :: Double -> Double -> String
bmiStatus weight height
  | weight / height ^ 2 <= 18.5 = "You are underweight!"
  | weight / height ^ 2 <= 25 = "You are with ideal weight!"
  | weight / height ^ 2 <= 30 = "You are overweight!"
  | otherwise = "You are obese!"


bmiStatus 85 1.81
"You are overweight!"


bmiStatus 80 1.81
"You are with ideal weight!"


bmiStatus 60 1.81
"You are underweight!"


bmiStatus 100 1.81
"You are obese!"


```
O *`Guards`* parece com *`Pattern Matching`*, mas nós podemos comparar valores e realizar ações se a comparação é verdadeira ou falsa. Ao contrário de *`Pattern Matching`* o qual avalia os padrões.

Mas nessa função onde estamos calculando se uma pessoa esta em forma ou não, comparando seu peso e altura, nós estamos repetindo três vezes o mesmo cálculo. Nós podemos melhorar isso usando *`where`*.
```haskell
bmiStatus' :: Double -> Double -> String
bmiStatus' weight height
  | bmi <= 18.5 = "You are underweight!"
  | bmi <= 25 = "You are with ideal weight!"
  | bmi <= 30 = "You are overweight!"
  | otherwise = "You are obese!"
  where bmi = weight / height ^ 2


bmiStatus’ 85 1.81
"You are overweight!"


bmiStatus’ 80 1.81
"You are with ideal weight!"


bmiStatus’ 60 1.81
"You are underweight!"


bmiStatus’ 100 1.81
"You are obese!"
```

Agora nós temos a nossa função mais simples e rápida porque o cálculo é feito uma vez só. Mas ainda podemos melhora-la fazendo-a mais legível e expressiva também:
```haskell
bmiStatus' :: Double -> Double -> String
bmiStatus' weight height
  | bmi <= skinny = "You are underweight!"
  | bmi <= normal = "You are with ideal weight!"
  | bmi <= fat = "You are overweight!"
  | otherwise = "You are obese!"
  where bmi = weight / height ^ 2
           (skinny, normal, fat) = (18.5, 25, 30)


```
Uma coisa que devemos estar concientes e tomar cuidado é que *`where`* tem escopo pelo corpo da função. Então se a mesma função tem dois corpos e apenas o último tem *`where`* a "variaveis" são somente disponíveis no segundo corpo e não em toda a função.
O *`where`* também pode ser usado com *`Pattern Matching`* quando queremos salvar valores em "variaveis". 

<br />

Hoje aprendemos sobre duas boas funcionalidades que nos ajudaram a escrever código em *`Haskell`*.
