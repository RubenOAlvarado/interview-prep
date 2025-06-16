# Components

Components are the building blocks of a React application. They are reusable pieces of code that define how a certain part of the UI should appear. Components can be either class-based or functional, with functional components being more common in modern React development due to their simplicity and the introduction of hooks.
Components can manage their own state and lifecycle methods, allowing for dynamic and interactive user interfaces. They can also accept inputs called "props" to render dynamic content. React encourages a declarative approach, where developers describe what the UI should look like based on the current state, and React takes care of updating the DOM efficiently.

## Table of Contents
| No. | Questions |
| --- | --------- |
| 1   | [Functional vs Class Components](#functional-vs-class-components) |
| 2   | [Component Lifecycle](#component-lifecycle) |
| 3   | [JSX and his relation with components](#jsx-and-his-relation-with-components) |
| 4   | [Differences between controlled and uncontrolled components](#differences-between-controlled-and-uncontrolled-components) |
| 5   | [How to pass data between components](#how-to-pass-data-between-components) |
| 6   | [How to split a component into smaller components](#how-to-split-a-component-into-smaller-components) |
| 7   | [Pure components](#pure-components) |
| 8   | [Prop drilling](#prop-drilling) |
| 9   | [Higher-order components](#higher-order-components) |


## Functional vs Class Components
The main difference between functional and class components in React lies in how they manage state and lifecycle methods and obviously in their syntax.
Functional components are simpler and are defined as JavaScript functions. They can use hooks to manage state and side effects, making them more concise and easier to read. Class components, on the other hand, are ES6 classes that extend `React.Component` and can have their own state and lifecycle methods.
Key differences include:
- **State Management**: Class components use `this.state` and `this.setState()` to manage state, while functional components use the `useState` hook.
- **Lifecycle Methods**: Class components have lifecycle methods like `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount`. Functional components use the `useEffect` hook to handle side effects.
- **Syntax**: Functional components are typically shorter and easier to read, while class components can be more verbose due to the need for `this` binding.
- **Use of `this`**: In class components, `this` refers to the component instance, while in functional components, `this` is not used, making them more straightforward.
- **Props**: Both types of components can accept props, but functional components can destructure props directly in the function parameters, making them cleaner.

<div align="right">
    <b><a href="#table-of-contents">↥ back to top</a></b>
</div>

## Component Lifecycle
The component lifecycle in React refers to the series of methods that are invoked at different stages of a component's existence, from creation to destruction. Understanding the lifecycle is crucial for managing side effects, optimizing performance, and ensuring proper resource management.
The lifecycle methods can be categorized into three phases:
1. **Mounting**: When a component is being created and inserted into the DOM.
2. **Updating**: When a component is being re-rendered due to changes in state or props.
3. **Unmounting**: When a component is being removed from the DOM.

<div align="right">
    <b><a href="#table-of-contents">↥ back to top</a></b>
</div>

### Example of a class component lifecycle:

```javascript
class MyComponent extends React.Component {
    // State initialization
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

    // Lifecycle methods
  componentDidMount() {
    console.log('Component mounted');
  }

  componentDidUpdate(prevProps, prevState) {
    console.log('Component updated');
  }

  componentWillUnmount() {
    console.log('Component will unmount');
  }

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Increment
        </button>
      </div>
    );
  }
}
```

<div align="right">
    <b><a href="#table-of-contents">↥ back to top</a></b>
</div>

### Example of a functional component lifecycle using hooks:

```javascript
import React, { useState, useEffect } from 'react';
function MyComponent() {
    const [count, setCount] = useState(0);

    // useEffect hook to mimic componentDidMount and componentDidUpdate
    useEffect(() => {
        console.log('Component mounted or updated');
        // cleanup function to mimic componentWillUnmount
        return () => {
            console.log('Component will unmount');
        };
    }, [count]); // Runs on mount and when count changes

    return (
        <div>
            <p>Count: {count}</p>
            <button onClick={() => setCount(count + 1)}>
                Increment
            </button>
        </div>
    );
}
```

<div align="right">
    <b><a href="#table-of-contents">↥ back to top</a></b>
</div>

## JSX and his relation with components
JSX (JavaScript XML) is a syntax extension for JavaScript that allows developers to write HTML-like code within JavaScript files. It is commonly used in React to describe the UI structure and is transformed into JavaScript function calls by tools like Babel.
JSX is closely related to components in React because it provides a way to define the structure and appearance of components in a declarative manner. Each JSX element corresponds to a React component, allowing developers to create complex UIs by composing smaller, reusable components.
JSX allows for a more intuitive and readable way to define the UI, as it closely resembles HTML. It supports embedding JavaScript expressions within curly braces `{}`, enabling dynamic content rendering based on component state or props.
JSX also supports nesting components, allowing developers to create a hierarchy of components that can be easily managed and reused. This composability is a key feature of React, enabling the creation of complex UIs from simple building blocks.

<div align="right">
    <b><a href="#table-of-contents">↥ back to top</a></b>
</div>

## Differences between controlled and uncontrolled components
Controlled and uncontrolled components in React refer to how form elements (like input fields) manage their state and handle user input.
### Controlled Components
Controlled components are form elements whose value is controlled by React state. The component's state is the single source of truth, and any changes to the input value are handled through event handlers that update the state. This allows for better control over the form data and makes it easier to implement validation and other logic.
### Example of a controlled component:
```javascript
import React, { useState } from 'react';
function ControlledInput() {
    const [value, setValue] = useState('');

    const handleChange = (event) => {
        setValue(event.target.value);
    };

    return (
        <input
            type="text"
            value={value}
            onChange={handleChange}
        />
    );
}
```
### Uncontrolled Components
Uncontrolled components, on the other hand, manage their own state internally. The value of the input is not controlled by React state, and instead, you can access the input value using a ref. This approach is less common in React but can be useful in certain scenarios where you want to avoid unnecessary re-renders or when integrating with non-React libraries.
### Example of an uncontrolled component:
```javascript
import React, { useRef } from 'react';
function UncontrolledInput() {
    const inputRef = useRef(null);

    const handleSubmit = (event) => {
        event.preventDefault();
        alert('A name was submitted: ' + inputRef.current.value);
    };

    return (
        <form onSubmit={handleSubmit}>
            <input type="text" ref={inputRef} />
            <button type="submit">Submit</button>
        </form>
    );
}
```

<div align="right">
    <b><a href="#table-of-contents">↥ back to top</a></b>
</div>

## How to pass data between components
In React, data can be passed between components using props (short for properties). Props are a way to pass data from a parent component to a child component, allowing for dynamic rendering and interaction within the UI. Here's how you can pass data between components:
### 1. Passing Data from Parent to Child
To pass data from a parent component to a child component, you can define the data as a prop in the parent and then access it in the child component.
### Example:
```javascript
import React from 'react';
function ParentComponent() {
    const message = "Hello from Parent!";

    return (
        <ChildComponent message={message} />
    );
}
function ChildComponent({ message }) {
    return (
        <div>
            <p>{message}</p>
        </div>
    );
}
```
### 2. Passing Data from Child to Parent
To pass data from a child component to a parent component, you can define a callback function in the parent and pass it as a prop to the child. The child can then call this function with the data it wants to send back to the parent.
### Example:
```javascript
import React, { useState } from 'react';
function ParentComponent() {
    const [childData, setChildData] = useState('');

    const handleDataFromChild = (data) => {
        setChildData(data);
    };

    return (
        <div>
            <ChildComponent onSendData={handleDataFromChild} />
            <p>Data from Child: {childData}</p>
        </div>
    );
}
function ChildComponent({ onSendData }) {
    const sendData = () => {
        onSendData("Hello from Child!");
    };

    return (
        <button onClick={sendData}>Send Data to Parent</button>
    );
}
```
### 3. Passing Data Between Siblings
To pass data between sibling components, you can lift the state up to their common parent. The parent can hold the shared state and pass it down to both siblings as props.
### Example:
```javascript
import React, { useState } from 'react';
function ParentComponent() {
    const [sharedData, setSharedData] = useState('');

    return (
        <div>
            <SiblingOne setSharedData={setSharedData} />
            <SiblingTwo sharedData={sharedData} />
        </div>
    );
}
function SiblingOne({ setSharedData }) {
    const sendData = () => {
        setSharedData("Data from Sibling One");
    };

    return (
        <button onClick={sendData}>Send Data to Sibling Two</button>
    );
}

function SiblingTwo({ sharedData }) {
    return (
        <div>
            <p>Data from Sibling One: {sharedData}</p>
        </div>
    );
}
```

<div align="right">
    <b><a href="#table-of-contents">↥ back to top</a></b>
</div>

## How to split a component into smaller components
Splitting a component into smaller components is a common practice in React to enhance code readability, maintainability, and reusability. Here are some steps and best practices to effectively split components:
1. **Identify Logical Units**: Look for sections of your component that can be logically separated based on functionality or UI structure. For example, if you have a form with multiple input fields, each field can be a separate component.
2. **Create Reusable Components**: If a part of your component is used in multiple places or has its own state and behavior, consider creating a reusable component. This helps avoid code duplication and makes your codebase cleaner.
3. **Props for Data Passing**: When splitting components, use props to pass data and functions between parent and child components. This allows child components to receive data from the parent and communicate back through callbacks.
4. **Maintain Component Hierarchy**: Ensure that the parent component manages the overall state and passes down necessary data to child components. This keeps the data flow unidirectional, which is a core principle of React.
5. **Use Composition**: React encourages composition over inheritance. Instead of creating complex class hierarchies, use functional components and compose them together to build your UI.
6. **Keep Components Focused**: Each component should have a single responsibility. If a component is doing too much, consider breaking it down further. This makes testing and debugging easier.

<div align="right">
    <b><a href="#table-of-contents">↥ back to top</a></b>
</div>

## Pure Components
Is a type of component in React that only re-renders when its props or state change. Pure components implement a shallow comparison of props and state, which can lead to performance optimizations by preventing unnecessary re-renders.

<div align="right">
    <b><a href="#table-of-contents">↥ back to top</a></b>
</div>

## Prop drilling
Prop drilling, refers to the process of passing data through multiple layers of components in React. This can lead to cumbersome code and make it difficult to manage state, especially when the data needs to be accessed by deeply nested components.
### Solutions to Prop Drilling
1. **Context API**: React's Context API allows you to create a global state that can be accessed by any component in the tree without having to pass props down manually. This is useful for sharing data like themes, user authentication, or settings across multiple components.
2. **State Management Libraries**: Libraries like Redux, MobX, or Zustand provide a more structured way to manage global state and avoid prop drilling. They allow you to store state in a central location and access it from any component without passing props through every level.
3. **Composition**: Instead of passing props through multiple layers, you can compose components in a way that allows them to access the necessary data directly from their parent or a higher-level component.

<div align="right">
    <b><a href="#table-of-contents">↥ back to top</a></b>
</div>

## Higher-order components
Higher-order components (HOCs) are functions that take a component and return a new component with additional functionality. They are a pattern in React for reusing component logic. HOCs can be used to enhance components by adding features like logging, data fetching, or state management without modifying the original component.

<div align="right">
    <b><a href="#table-of-contents">↥ back to top</a></b>
</div>