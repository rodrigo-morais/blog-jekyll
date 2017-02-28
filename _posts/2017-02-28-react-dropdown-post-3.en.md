---
layout: post
title: React - Creating a Dropdown component - Part 3
published: true
lang: en
translation: false
---

Hey folks!

After a vacation I’m back and I’d like to still work in this component with you.

In the second post we start to build the *`Trigger`* component to our dropdown. Now we will continue building it.
<!--more-->
<br />

**Standard text or Not**

We started testing when our component receive a text if it is presented correctly. But if our component doesn’t receive a text should we present a blank string to the user or we can have a default text for this case.
I think that it is a team decision because we have to decide as team if we will trust in the *`PropTypes`* and follow their warnings as errors or not. Because the *`PropTypes`* in our *`Trigger`* is saying that the text is required.
If we will trust the *`PropTypes`* then every time that we have a warning we will fix it. On the other hand if we not rely the *`PropTypes`* we have to write a defensive code to our component.
Let’s take a look in the two scenarios.

<br />

***Defensive Code***

In this case we will rewrite our test when we inform a text to the *`Trigger`* component.
Let’s start creating a context to it and put our test inside:

```javascript
describe('Trigger Component', () => {
  const text = 'Select Something';
  const props = { text };
  let trigger;

  context('when text is informed', () => {
    beforeEach(() => {
      trigger = shallow(<Trigger {...props} />);
    });

    it('renders a text', () => {
      expect(trigger.props().children).to.be.equal(text);
    });
  });
});
```
Our test now is passing the text as *`Select Something`* and not just select, because the *`Select`* text will be our default text. If we run the test it still passing.
So let’s add a new context when the text is not informed:
```javascript
context('when text is not informed', () => {
    beforeEach(() => {
      trigger = shallow(<Trigger />);
    });

    it('renders a default text when the text is not informed', () => {
      const defaultText = 'Select';

      expect(trigger.props().children).to.be.equal(defaultText);
    });
  });
```
Now we are not informing the text, but we are asserting that the text is *`Select`* because it is our default text which will be presented when we not inform the text as props.
If we run the tests this new one will break, because our *`Trigger`* component doesn’t have a default text.
Let’s add a default text to our component:
```javascript
import React, { PropTypes } from 'react';

function Trigger({ text = 'Select' }) {
  return (
    <a>{text}</a>
  );
}

Trigger.propTypes = {
  text: PropTypes.string.isRequired
};

export default Trigger;
```
This version of our component is receiving *`Select`* as default text and if we run the tests again all will pass.  

What happens if our text is *`undefined`* or *`null`*? Is a default text enough to these cases?
Let’s see what happens when the text is *`undefined`*.
```javascript
context('when text is undefined', () => {
    const defaultText = 'Select';

    it('renders a default text when the text is undefined', () => {
      const text = undefined;
      const props = { text };

      trigger = shallow(<Trigger {...props } />);

      expect(trigger.props().children).to.be.equal(defaultText);
    });
  });
```
If we run the tests the new one will pass and we don’t need change our code. But if the text receives null?
```javascript
it('renders a default text when the text is null', () => {
      const text = null;
      const props = { text };

      trigger = shallow(<Trigger {...props } />);

      expect(trigger.props().children).to.be.equal(defaultText);
    });
```
When we run this test we receive an error because the code in our *`Trigger`* component is not enough to guarantee that we will present the default text.
Easily we can fix it just adding more one defensive code in our component:
```javascript
import React, { PropTypes } from 'react';

function Trigger({ text = 'Select' }) {
  return (
    <a>{ text || 'Select' }</a>
  );
}

Trigger.propTypes = {
  text: PropTypes.string.isRequired
};

export default Trigger;
```
And we run the tests and all will pass.  

We cover how to treat the props when we don’t trust in the component’s *`PropTypes`*.

<br />

**PropTypes warnings**

*`React`* already add to us some warnings when a *`PropType`* is not informed. These warnings are presented when we run our tests and in the Browser console.
We can test it. Returning to original code before we had add the defensive code we can test it in our tests. Let’s add a new test where we don’t pass the *`text`* property to our *`Trigger`* component.
```javascript
it('renders a text 2', () => {
    const trigger2 = shallow(<Trigger />)
    expect(trigger2.props().children).to.be.equal(undefined)
  })
```
And now when we run our tests we can see a warning like: *Warning: Failed prop type: The prop `text` is marked as required in `Trigger`, but its value is `undefined`.*  

This same warning will appear in the Browser console if we don’t pass *`text`* to our component when we use it.  

In this case we have to be always aware for these warnings and not accept them to make our code reliable.  

**Conclusion**

In the end the decision of the best approach is from the team. Each team can think that one approach is better than another and there isn’t anything wrong in that.  

To our component we will rely in the *`PropTypes`* warnings and never accept them.
