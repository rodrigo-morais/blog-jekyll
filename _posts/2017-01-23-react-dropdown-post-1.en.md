---
layout: post
title: React - Creating a Dropdown component - Post 1
published: true
lang: en
translation: false
---

Hey folks!

I’m working with [*`React`*](https://facebook.github.io/react/), which is a JavaScript library to build user interfaces, in the last months and I guess there are really some subjects that we can discuss here.  
My previous project was a website to booking air tickets to the biggest air company in South America and my current project is a language learning app. In the previous project we had really complex *`React`* components which gave a lot of fun to work with, and my current project has more simpler components with more focus in the presentation. In the last week a work in a component that have more user interaction and this kind of component is a good one to discuss here because it has some details which worth to discuss.  
<!--more-->
So, in the next posts we will build a dropdown where we can select some information. This is the idea of our component, and we have some requirements for it:

The trigger to open the dropdown should be a link with an icon beside;
When the dropdown is opened and the link(trigger) is clicked it must close;
When the dropdown is opened and is clicked in other element it must close;
When one item of the list is selected it should call an external callback;
Items can or can’t have images beside;
Items always have a text;
Accessibility:
User can navigate with keyboard;
Must be navigable using a screen reader;
Tests:
Unit;
Integration;
Functional;

These are the requirements to our component.  

<br />

**Configuration**

Today we will start just creating a simple configuration to the first interaction. After in each new interaction we will add new libraries to it if was necessary.  
So to begin we create a *`package.json`* file where we are installing *`React`*, *`Webpack`*, *`ESLint`* and *`Babel`*.  
Beyond that we configure the *`Webpack`*:
```javascript
module.exports = {
  entry: './app/main.js',
    output: {
      path: './dist',
      filename: 'index.js'
    },
  devServer: {
    inline: true,
    port: 3333
  },
  module: {
    loaders: [
      {
        test: /\.jsx?$/,
        exclude: /node_modules/,
        loader: 'babel-loader',
        query: {
          presets: ['es2015', 'react', 'stage-0'],
          plugins: ["transform-object-rest-spread"]
        }
      }
    ]
  }
}
```
And the *`ESLint`*. To configure the *`ESLint`* we call a command:
```shell
./node_modules/.bin/eslint --init
```
This command will ask us some questions and will create a *`.eslintrc.*`* file. We add some configurations to this file:
```javascript
{
    "extends": "airbnb",
    "plugins": [
        "react",
        "jsx-a11y",
        "import"
    ],
    "rules": {
      "comma-dangle": ["error", "never"],
      "semi": [2, "never"]
    }
}
```
These are the basic configurations to our *`lint`* and in the next postis we will improve it.

<br />

It is enough to start our project. In the next post we will start to build our dropdown.  
You can see the code [here](https://github.com/rodrigo-morais/react-dropdown/tree/post-1).
