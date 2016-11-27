---
layout: post
title: Using local storage with React and Redux
published: false
lang: en
---

Usually our application starts `Redux's` store with an empty object to show that the application doesn't any have data when it starts. In the future when users have some interaction or when the application get some data from the back-end so the store will keep these data. It is the most commom way to use `Redux` in a `React` project, at least in the projects which I worked til now, but sometimes we need another approach.
To create a store with `Redux` we have to use a function called `createStore` which should be imported from `Redux` and pass as a parameter our `reducers`.

Ok, first we can use as an example a reducer for a TODO application. Probably we have a file called `reducers.js` to create it.

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

With this reducer we can create a store. To do it we have to import the `createStore` function from `Redux` and our `reducers` in the file which we are creating the store, which probably is called `app.js` or something similar.

```javascript
import reducers from './reducers'
import { createStore } from 'redux'

export const store = createStore(reducers)
```

Now we have our store with a TODO list which was initialized with empty array ([]).

Ok, it works pretty well. But in this case every time that our application is reloaded we lose all TODOs which we registered. If we have to keep they we have to save these TODOs in some storage.
Let's think a little bit more and say that we have a more complex application which get some data from the back-end and they are not changed soon and we want to keep they when we reload the page. How can we do it?
One solution to this situation is to use the `local storage` which is a small "database" inside our browser.

Let's take a look how todo that in our TODO app.

First we have to create two functions to get data from the local storage and to save data there.
For it we can create a file called `localStorage.js` where we will have these functions.

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

To use the local storage is pretty simple, it works as a list of key-values. When we want get data we call the function `getItem` from the global object called `localStorage` passing the key as a parameter. And to save data we call the function `setItem` from the same global object passing the key and the data.
The data in local storage have to be always serialized and because of that when we load the data we have to deserialize using `JSON.parse` and when we send data we have to serialize they with `JSON.stringify`.
Another point is that sometimes the local storage hasn't permission to be accessed or for other reason we can get an error. Because of that, we have to use a try/catch when call functions from local storage.

Now we have to use our functions to save and load data from the local storage to our application.
In our `app.js` file we will import our `localStorage.js` file and use its functions.

```javascript
import { saveState, loadState } from './localStorage'

export const store = createStore(reducers, loadState())

store.subscribe(() => {
  saveState({
    todos: store.getState().todos
  })
})
```

Now in the function `createStore` we are passing a second parameter which is the return of the function `loadSotre` that we created to get the data from local storage. The function `createStore` from `Redux` accepts to receive data to hydrate the store. Take a look in the [documentation](https://github.com/reactjs/redux/blob/master/docs/api/createStore.md).
To save the data in the local storage we are using a function called `subscribe` from the store, which will be called every time when store is modified. For this function we are passing a function which call the `saveState` function which we created before and it will receive a new state of todos to be save in local storage.

With this new implementation we can save data in the local storage and reuse data without hit on the back-end every time that we reload our app and still use til we close the browser or browser's tab.

If you want test this approach, please, take a look in this [repository](https://github.com/rodrigo-morais/react-redux-to-do).
