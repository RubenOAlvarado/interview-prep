# Javascript frequently asked questions

## Table of Contents

| No. | Questions |
| --- | --------- |
| 1   | [What is JavaScript?](#what-is-javascript) |
| 2   | [Explain the difference between `var`, `let`, and `const`.](#explain-the-difference-between-var-let-and-const) |
| 3   | [Explain the difference between `null` and `undefined`.](#explain-the-difference-between-null-and-undefined) |
| 4  | [What's the difference between deep and shallow copy?](#whats-the-difference-between-deep-and-shallow-copy) |
| 5   | [Interview Question: Shallow or Deep Copy?](#interview-question-shallow-or-deep-copy) |
| 6   | [Explain the concept of currying in JavaScript.](#explain-the-concept-of-currying-in-javascript) |
| 7   | [Interview Question: Currying Example](#interview-question-currying-example) |
| 2   | [Recommended Reading](#recommended-reading) |

### What is JavaScript?
JavaScript is a high-level, dynamic, untyped, and interpreted programming language. It is a core technology of the World Wide Web, alongside HTML and CSS, and enables interactive web pages. JavaScript is an event-driven, functional, and imperative language known for its versatility in both client-side and server-side development.

### Explain the difference between `var`, `let`, and `const`.
`var`, `let`, and `const` are all used to declare variables in JavaScript, but they have different scopes and behaviors:
- `var`: Declares a variable that is function-scoped or globally scoped. It can be re-declared and updated.
- `let`: Declares a block-scoped variable that can be updated but not re-declared within the same scope.
- `const`: Declares a block-scoped variable that cannot be updated or re-declared. It must be initialized at the time of declaration.

### Explain the difference between `null` and `undefined`.
`null` is an assignment value that represents the intentional absence of any object value. It is a primitive value that can be assigned to a variable to indicate that it has no value. `undefined`, on the other hand, is a type itself and indicates that a variable has been declared but has not yet been assigned a value. In other words, `undefined` means a variable exists but has no value, while `null` is an explicit assignment of no value. 

### What's the difference between deep and shallow copy?
A shallow copy creates a new object that is a copy of the original object, but it only copies the references to the nested objects. If the nested objects are modified, the changes will reflect in both the original and copied objects. A deep copy, however, creates a new object and recursively copies all nested objects, ensuring that changes to the nested objects in the copied object do not affect the original object.

### Interview Question: Shallow or Deep Copy?
What does this code output?
```javascript
const original = { 
  name: "Alice", 
  hobbies: ["coding", "hiking"], 
  address: { city: "Berlin" } 
};
const shallowCopy = { ...original };
shallowCopy.name = "Bob";
shallowCopy.hobbies.push("reading");
shallowCopy.address.city = "Munich";
console.log(original.name); // What will this output?
console.log(original.hobbies); // What will this output?
console.log(original.address.city); // What will this output?
```

**Answer:**
```bash
Alice
[ 'coding', 'hiking', 'reading' ]
Munich
```

**Explanation:**
1. Primitive: (`.name`): The `name` property is a primitive value, so changing it in the `shallowCopy` does not affect the `original` (primitives are copied by value).
2. Reference: (`.hobbies`): The `hobbies` property is an array (a reference type), so pushing a new value into it in the `shallowCopy` affects the `original` (arrays are copied by reference).
3. Nested Object: (`.address.city`): The `address` property is an object (a reference type), and changing a property within it in the `shallowCopy` affects the `original` (nested objects are copied by reference).

**Key Takeaway:**
Shallow copies copy references to nested objects, so changes to nested properties in the copied object will affect the original object. In contrast, deep copies create entirely new objects, preventing any changes in the copied object from affecting the original.
The spread operator (`...`) creates a shallow copy of the `original` object, meaning that while the top-level properties are copied, nested objects and arrays are still referenced. Therefore, modifications to nested properties in the `shallowCopy` will reflect in the `original` object.

### Explain the concept of currying in JavaScript.
Currying is a functional programming technique in JavaScript where a function is transformed into a sequence of functions, each taking a single argument. This allows for partial application of functions, enabling the creation of more specialized functions from general ones. Currying can improve code readability and reusability by allowing functions to be called with fewer arguments over time.

### Interview Question: Currying Example
What does this code output?
```javascript
const multiply = (x) => (y) => x * y;

const double = multiply(2);
const triple = multiply(3);

console.log(double(5)); // What will this output? 
console.log(triple(double(2))); // What will this output?
```

**Answer:**
```bash
10
12
```

**Explanation:**
1. Breakdown:
    - `multiply` is a curried function that takes `x` and return a function waiting for `y`.
    - `double = multiply(2)` remembers `x=2` and wait for `y`.
    - `triple = multiply(3)` remembers `x=3` and wait for `y`.
2. First Log(`double(5)`):
    - Calls `double` with `5`, which is `multiply(2)(5)`.
    - Returns `2 * 5 = 10`.
3. Second Log(`triple(double(2))`):
    - Calls `double(2)`, which is `multiply(2)(2)`.
    - Returns `2 * 2 = 4`.
    - Then calls `triple(4)`, which is `multiply(3)(4)`.
    - Returns `3 * 4 = 12`.

**Key Takeaway:**
Currying allows functions to be broken down into smaller, reusable functions that can be called with fewer arguments, enhancing modularity and readability. In this example, `double` and `triple` are specialized functions derived from the general `multiply` function.

### Recommended Reading
- [JavaScript Basics](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps)
- [JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
- [Javascript Info](https://www.javascript.info/)