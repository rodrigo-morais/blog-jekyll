---
layout: post
title: Using local storage with React and Redux
published: true
lang: pt_BR
translation: true
---

Geralmente nosssas applicações iniciam o *`Redux's`* store com um objeto vazio para mostrar que a aplicação não tem nenhum dado ao ser iniciada. No futuro quando usuários tiverem alguma interação ou quando a aplicação receber dados do back-end então o store irá manter esses dados. Essa é uma abordagem muito comum para usar *`Redux`* em um projeto *`React`*, ao menos em projetos no qual eu trabalhei até agora, mas as vezes nós necessitamos uma outra abordagem.

Para criar um store com *`Redux`* nós temos que usar uma função chamada *`createStore`* qual nós importamos do *`Redux`* e passamos como parâmetro os nossos *`reducers`*.

<!--more-->

Ok, primeiro nós podemos usar como um exemplo um *`reducer`* para uma aplicação TODO. Provavelmente nós temos um arquivo chamado *`reducers.js`* para cria-lo.

```javascript
export const todos = (state = [], action) => {
  switch (action.type) {
    case ADD_TODO:
      // add new todo
    case REMOV_TODO:
      // remove todos
    default:
      state
  }
}
```

Com esse *`reducer`* nós podemos criar uma store. Para fazer isso nós temos que importar a função *`createStore`* do *`Redux`* e nossos *`reducers`* em um arquivo no qual nós criamos o store, que provavelmente se chama *`app.js`* or algo similar.

```javascript
import reducers from './reducers'
import { createStore } from 'redux'

export const store = createStore(reducers)
```
Agora nós temos nossa store com um TODO list qual foi inicializado com um array vazio ([]).

Ok, isso funciona muito bem, Mas nesse caso toda a vez que nossa aplicação é recarregada nós perdemos todos os TODOs que foram cadastrados. Se nós temos que mante-los, nós temos que salva-los em alguma base de dados.
Vamos pensar um pouco mais e dizer que nós temos uma aplicação mais complexa que busca dados do back-end e eles não serão alterados em um curto espaço de tempo e por isso queremos mante-los quando a página for recarregada. Como podemos fazer isso?
Uma solução para essa situação é usar *`local storage`* que é um pequeno "database" dentro do browser.

Vamos ver como fazer isso na nossa TODO app.

Primeiro nós temos que criar duas funções para obter dados do local storage e para salvar os dados lá.
Para isso nós podemos criar um arquivo chamado *`localStorage.js`* onde nós teremos essas funções.

```javascript
export const loadState = () => {
  try {
    const serializedState = localStorage.getItem('state')
    if (serializedState === null) {
      return undefined
    }
    return JSON.parse(serializedState)
  }
  catch (err) {
    return undefined
  }
}

export const saveState = (state) => {
  try {
    const serializedState = JSON.stringify(state)
    localStorage.setItem('state', serializedState)
  }
  catch (err) {
    // ignore
  }
}
```

Para usar o local storage é muito simples, ele é uma lista de chave-valor. Quando nós queremos obter dados nós chamamos a função *`getItem`* do objeto global chamado *`localStorage`* passando a chave como parâmetro. E para salvar dados nós chamamos a função *`setItem`* do mesmo objeto global passando a chave e os dados.
Os dados no local storage devem sempre ser serializados e por causa disso quando carregamos os dados nós temos que deserializa-los usanso *`JSON.parse`* e quando enviamos dados nós temos que serializa-los com *`JSON.stringify`*.
Outro ponto importante é que o local storage pode não ter permissão de acesso ou outro erro pode acontecer ao tentar acessa-lo. Por isso o código de acesso ao local storage deve estar dentro de um bloco try/catch.

Agora nós temos que usar as funções para salvar e carregar dados do local storage na nossa aplicação.
No nosso arquivo *`app.js`* nós iremos importar nosso arquivo *`localStorage.js`* e usar suas funções.

```javascript
import { saveState, loadState } from './localStorage'

export const store = createStore(reducers, loadState())

store.subscribe(() => {
  saveState({
    todos: store.getState().todos
  })
})
```

Agora na função *`createStore`* nós estamos passando um segundo parâmetro que é o retorno da função *`loadStore`* que criamos para obter dados do local store. A função *`createStore`* do *`Redux`* aceita receber dados para hidratar o store. De uma olhada na [documentação](https://github.com/reactjs/redux/blob/master/docs/api/createStore.md).
Para salvar os dados no local storage nós usamos a função chamada *`subscribe`* do store, que será chamada toda vez que o store for modificado. Para essa função nós estamos passando uma função que chama a função *`saveState`* que criamos anteriormente e irá receber o estado dos TODOs para serem salvos no local storage.

Com essa nova implementação nós podemos salvar dados no local storage e reusa-los sem ter que acessar o back-end a todo momento que recarregamos a aplicação até que o browser ou aba sejam fechados.

Se você quiser testar essa abordagem, de uma olhada nesse [repositório](https://github.com/rodrigo-morais/react-redux-to-do).
