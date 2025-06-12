# React frequently asked questions

## Table of Contents

| No. | Questions |
| --- | --------- |
| 1   | [What is React?](#what-is-react) |
| 2   | [What are the advantages of using React?](#what-are-the-advantages-of-using-react) |
| 3   | [What are the limitations of React?](#what-are-the-limitations-of-react) |
| 4   | [What is JSX?](#what-is-jsx) |
| 5   | [What is the Virtual DOM?](#what-is-the-virtual-dom) |

## Topics
- [Components](components.md)
- [State and Props](state-and-props.md)
- [Hooks](hooks.md)

## What is React?
React is an open-source JavaScript library for building user interfaces, particularly single-page applications where you need a fast, interactive user experience. It allows developers to create large web applications that can change data without reloading the page. React is maintained by Facebook and a community of individual developers and companies. It uses a component-based architecture, enabling the creation of reusable UI components.
React employs a virtual DOM to optimize rendering performance, making it efficient for dynamic applications. It supports both client-side and server-side rendering, enhancing SEO capabilities. React's ecosystem includes tools like React Router for routing and Redux for state management, making it a powerful choice for modern web development.

## What are the advantages of using React?
React offers several advantages for web development:
- **Component-Based Architecture**: Encourages reusable UI components, making code more maintainable and scalable.
- **Virtual DOM**: Enhances performance by minimizing direct manipulation of the actual DOM, leading to faster updates and rendering.
- **Unidirectional Data Flow**: Simplifies debugging and understanding of data flow within the application.
- **Rich Ecosystem**: Provides a wide range of libraries and tools, such as React Router for navigation and Redux for state management.
- **Strong Community Support**: Backed by Facebook and a large community, ensuring continuous improvement and a wealth of resources.
- **SEO Friendly**: Supports server-side rendering, improving search engine optimization for web applications.

## What are the limitations of React?
While React has many advantages, it also has some limitations:
- React is not a complete framework; it is only a library.
- The components in React are numerous and will take time to fully grasp the benefits of all.
- It might be difficult to learn for beginners, especially those without a strong JavaScript background.
- Coding might become complex as it will make use of inline templates and JSX.

## What is JSX?
JSX (JavaScript XML) allows to write HTML inside Javascript and place them in the DOM without using functions like `createElement()`. 
It provides syntactic sugar for `React.createElement()` function.

## What is the Virtual DOM?
A virtual representation of the real DOM that is kept in memory and synced with the real DOM by a library such as ReactDOM.

### How does it work?
For every DOM object, there is a corresponding virtual DOM object. Consider a virtual DOM object as a blueprint of the real DOM object. When a JSX element gets rendered, every virtual DOM object is updated. React then compares the new virtual DOM with the previous one and calculates the difference (diffing). It then updates only the parts of the real DOM that have changed, which is more efficient than re-rendering the entire DOM.