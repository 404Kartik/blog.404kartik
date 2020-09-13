---
layout: post
title:  "ReactJs "The Hello World"
description: Getting started with ReactJs
date:   2020-09-13 21:03:36 +0530
categories: ReactJs Web-Develoment 
---

## Why use React ?

As already mentioned in the introduction we now know that it is a javascript library to build beautiful user interfaces. React is also:

1. **_Declarative:_** We as developers just need to focus on designing views for each state change in our application. React will update and render the right components when the data changes. The code becomes more predictable and easy to debug.
2. **_Component-Based:_** In component based approach we encapsulate behaviours into small units called components. They manage their own state.This make the code easy by splitting the logic into reusable independent code.
3. **_Technology-stack agnostic:_** React does not care what tech-stack you use. You can develop new features in React without rewriting code. It can render on the server using node.

### Let's cut the chase and dive into real code examples

## Hello World with React

Now that you have a basic knowledge of the main concepts of React, it's time to see a concrete example. Let's start by creating a new `index.html` file containing the following code:
    
    
    
       
          
       
       
          http://www.google-analytics.com/ga.js"> src="">https://fb.me/react-0.12.2.js">
          ">https://fb.me/JSXTransformer-0.12.2.js">
          ">https://www.telerik.com/hello.jsx">
          ">https://www.telerik.com/main.jsx">
      
The code below is our `hello.jsx` component:
    
    
    var Hello = React.createClass({
       render: function() {
          return 
Hello, world!

;
       }
    });

In the above snippet, we've created a new React component by passing an object literal to the `React.createClass()` method, which implements the Factory pattern. The result of invoking this method is stored in a variable named `Hello`. Inside the object literal, we define a property called `render` which has a function as its value.

As I mentioned, `render()` is responsible for creating the objects that display the HTML code resulting from the component. However, instead of using a statement like `console.log()`, `alert()` or `document.write()`, we return the content to display. Here we're returning a paragraph with "Hello, world!".


Hello, {this.props.name}
;
      }
    }
    
    
    function Welcome(props) {
      return 
Hello, {props.name}
;
    }

## State

React has a built-in state object where we store property value that belongs to the component.
    
    
    class Car extends React.Component {
      constructor(props) {
        super(props);
        this.state = {brand: "Ford"};
      }
      render()
    }


## Getting Started with React



Prerequisites : 

1. Node.js

Before starting with the project make sure you have node version >= 8.10 installed on your system. You can install it using these commands
    
    
    sudo apt-get update
    sudo apt-get install nodejs

You will also want to install the Node.js package manager. You can do this by using :
    
    
    sudo apt-get install npm
    

We're using this _ES6_ syntax to define our new _Greeter_ component, and it is an extension of the basic React component. (The reason we might choose to use this syntax over React's own component declaration method is purely aesthetic at this point of the tutorial, [_but there is a fundamental difference_][6].)

We'll explore the full implication of this declaration in later parts of the tutorial, but essentially it means, '_Give me a named container for everything I want to do with my component_.' In the future, you might add functionality for say, connecting with a data source, or even reacting to changes in your app state (geddit now?!) For now, all we want to look it is outputting a piece of our UI:
    
    
    render() {   
    **return** 
{**this**.props.greeting}
  
    }

So far, so vanilla Javascript. Every React component must return something for React to _render, _or output, to the DOM (Ed: It's OK to return _null_.) And this is what our render method is doing: returning an _h1_ tag.

But what is that? Between the curly brackets? The _h1 _tag contains what looks like non-HTML. That's part of the JSX syntax! In this case, the curly brackets are telling React to parse the Javascript inside the brackets and render them as the content inside the tag:
    
    
    {**this**.props.greeting}

We'll look at exactly what '_this_' means, and what '_props_' are in later parts, but what you should now is that '_props_' is short for '_properties_'. You can look at properties as pieces of data that are passed down from a parent component.

JSX can do more than simply render passed data, though. As we go through the course, you'll see how we can express ourselves to achieve the nested nature of components, pass data and functions, and keep the turtles going all the way down.
    
    
    ReactDOM.render(, document.getElementById('myReactApp'));

Finally, the line that brings it all together, and you can see more JSX! _ReactDOM _is the Javascript library object that you import and use to tie your React app to the real DOM. Here we tell ReactDOM to '_render_' our new component and attach it to the root element which we can find using the standard Javascript DOM method '_document.getElementById_.'
