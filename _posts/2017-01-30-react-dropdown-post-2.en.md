---
layout: post
title: React - Creating a Dropdown component - Part 2
published: true
lang: en
translation: false
---

Hey folks!

In the first part we saw how configure our project to build a component using *`React`*.  
Today we will start to build our component. Our dropdown is compounded from small components building in the end the final component which is our dropdown.  
I defend that always when we build a component as a dropdown we have to do that thinking as a third party component but just having what is really necessary and not trying to predict what the component will need in the future.
<!--more-->

<br />

**Puzzle**

A component in *`React`* is a puzzle where we match small components to have our final product. Our dropdown is one of this cases, we have some small components to build it. For example, a dropdown has a trigger which is an element that the user can interact to open nor close the dropdown. Another component could be a list of items inside our dropdown and depending how complex is each item we can extract a new component from it.

<br />

**Third Party component**

Majority of components that we build can be reused in our project, in different projects or even for other teams. The cost to create a generic component is not much bigger than create an exclusive one to our problem, at least in the majority of the cases. Because of that, I defend the idea to create third party components to be reused.

<br />

**First Component**

We will start building a trigger to our dropdown. The requirements are:  
* A text which should be configurable
* A icone as an arrow showing if the dropdown is opened or closed
* A click event which open or close the dropdown

We should start our trigger component as much simple as possible and in each new interaction we can improve it. Is very common when we start to compound the components to work together realize that we need add more features in them.  

This is the visual idea that I have to our component:

<image src="{{site.url}}/images/react_1.png" />

<br />

**TDD**

We will use *`TDD`* to build our trigger. This wants to say that we will write tests before write the component’s code to them guide our design.  
To do it we have to import some libraries:
```shell
npm i --save-dev mocha
npm i --save-dev chai
npm i --save-dev enzyme
npm i --save-dev babel-plugin-module-resolver
npm i --save-dev react-addons-test-utils
```
Here we are importing [*`Mocha`*](https://mochajs.org/) which is a good framework to write JavaScript tests, [*`Chai`*](http://chaijs.com/) which is an assertion library to complement *`Mocha`* and [*`Enzyme`*](https://github.com/airbnb/enzyme) that is a library to test *`React`* components.  
We are importing a plugin to Babel which we will configure to say where are the source files and can use relative path to them in our tests.  And we importing a *`React`* plugin called *`react-addons-test-utils`* which make easier create tests.

Beyond that we will add an script to our *`package.json`* file to make the action of run tests easier:
```javascript
"test": "npm run test:unit",
"test:unit": "./node_modules/mocha/bin/mocha --opts spec/mocha.opts",
```
And we have a file called *`mocha.opts`* with some *`Mocha`*’s configurations:
```javascript
-inline-diffs
--reporter spec
--compilers js:babel-register
spec/**/*Spec.js
```
In this file we are saying to *`Mocha`* where are our tests and that we are using *`Babel`* to transpile our code.

The last configuration is the *`.babelrc`* file where we configure the presets and plugins:
```javascript
{
  "presets": ["es2015", "react"],
  "plugins": [
    [
      "module-resolver", {
        "root": ["./src/"],
        "alias": {
          "src": "./src"
        }
      }
    ]
  ]
}
```

<br />

**First requirement**

Let’s start testing if the text which we pass to our trigger is exhibited or not. This is the test:
```javascript
import { expect } from 'chai';
import React from 'react';
import Trigger from 'src/components/Trigger';
import { shallow } from 'enzyme';

describe('Trigger Component', () => {
  const text = 'Select';
  const props = { text };
  const trigger = shallow(<Trigger {...props} />);

  it('renders a text', () => {
    expect(trigger.props().children).to.be.equal(text);
  });
});
```
We created the test in this path: *`spec/components/TriggerSpec.js`*  
In this test we are importing the libraries *`React`*, *`chai`*, *`enzyme`* and our component. Then we use *`shallow`* from *`enzyme`* to build our component and we verify that the text which we passed is contained in our component. If we run the test now it must fail because we don’t have the *`Trigger`* component.  
Let’s build it:
```javascript
import React, { PropTypes } from 'react';

function Trigger({ text }) {
  return (
    <a>{text}</a>
  );
}

Trigger.propTypes = {
  text: PropTypes.string.isRequired
};

export default Trigger;
```
Our component was created in this path: *`src/components/Trigger.js`*  
Right now this component is really simple and we even don’t need create a component to it. But when we add more features this component will make sense.  

If we run the test now it will pass:
```shell
npm test
```

<br />

And now we have our component with the first requirement. 
You can see the code [here](https://github.com/rodrigo-morais/react-dropdown/tree/post-2).  
In the next post we will add the other requirements.
