# React.js

### Q : What is React?  
A : React is an open-source JavaScript library developed by Facebook for building interactive user interfaces, especially for single-page applications (SPAs). It allows developers to create UI using independent and reusable components.

* Used for building dynamic web applications.
* Focuses only on the view layer of an application (UI).
* Allows UI to be built using small reusable components.
* Can be used to build web and mobile applications.

### Q : Features of React.  
A :  
* Uses **JSX**, a JavaScript syntax extension that allows writing HTML-like code in JS.  
* Implements **Virtual DOM** for efficient updates and improved performance.  
* Supports **server-side rendering (SSR)**, enhancing SEO.  
* Follows **one-way data binding**, making state management predictable.  
* Promotes **component reusability**, allowing for modular UI development.  

### Q : What are the advantages of using React?  
A :  
* **High performance** due to Virtual DOM optimizations.  
* **JSX** makes code more readable and maintainable.  
* **Server-side rendering (SSR)** improves SEO and initial load time.  
* **Easy integration** with other frameworks like Angular or Backbone.  
* **Simplifies testing** with tools like Jest for unit and integration tests.  

### Q : What is JSX?
A : With help of babel library jsx code gets convert to js code that browser can understand. Babel is a transpiler.

JSX stands for JavaScript XML. It allows us to write HTML inside JavaScript and place them in the DOM without using functions like appendChild( ) or createElement( ). As stated in the official docs of React, JSX provides syntactic sugar for React.createElement( ) function.

Note- We can create react applications without using JSX as well.

Let’s understand how JSX works:
```
const container = (
<div>
  <p>This is a text</p>
</div>
);
ReactDOM.render(container,rootElement);
```
### Q : What is memory leak in react?
A :
A **memory leak** in React (or in any JavaScript application) happens when your app **keeps holding onto memory that is no longer needed**, leading to **increased memory usage** over time. This can eventually cause **performance issues**, such as slow interactions or even crashes.

### **How Do Memory Leaks Happen?**
Memory leaks in React often occur when:
1. **An asynchronous task (like an API call or a timer) continues running after a component unmounts.**
2. **Event listeners are not properly removed** when a component unmounts.
3. **Global variables or references** to objects persist in memory, preventing garbage collection.
4. **Using `setState` on an unmounted component**, causing React to keep a reference to that component in memory.

## **Common Causes of Memory Leaks in React**
### ** API Requests Without Cleanup**
#### **Example: Memory Leak**
If an API request is still in progress when a component unmounts, and it tries to update state, a memory leak occurs.

```jsx
import { useState, useEffect } from "react";
import axios from "axios";

function MyComponent() {
  const [data, setData] = useState(null);

  useEffect(() => {
    axios.get("/api/data").then((response) => {
      setData(response.data); // ❌ Could try to update state after unmount
    });

    // No cleanup function here!
  }, []);

  return <div>{data}</div>;
}
```
#### **Fix: Add Cleanup**
To **prevent updating state on an unmounted component**, we use a **flag** or **AbortController**.

```jsx
import { useState, useEffect } from "react";
import axios from "axios";

function MyComponent() {
  const [data, setData] = useState(null);

  useEffect(() => {
    let isMounted = true;

    axios.get("/api/data").then((response) => {
      if (isMounted) {
        setData(response.data);
      }
    });

    return () => {
      isMounted = false; // Cleanup when unmounting
    };
  }, []);

  return <div>{data}</div>;
}
```
Alternatively, **AbortController** can be used to cancel the request:
```jsx
useEffect(() => {
  const controller = new AbortController();
  axios.get("/api/data", { signal: controller.signal })
    .then(response => setData(response.data))
    .catch(error => {
      if (error.name !== "AbortError") {
        console.error(error);
      }
    });

  return () => controller.abort(); // Cancels request on unmount
}, []);
```
### ** Event Listeners Not Removed**
#### **Example: Memory Leak**
```jsx
useEffect(() => {
  window.addEventListener("resize", () => {
    console.log("Resizing...");
  });

  // ❌ No cleanup function - event listener stays in memory
}, []);
```
#### **Fix: Remove Event Listener on Unmount**
```jsx
useEffect(() => {
  const handleResize = () => console.log("Resizing...");
  window.addEventListener("resize", handleResize);

  return () => {
    window.removeEventListener("resize", handleResize);
  };
}, []);
```

### ** Timers (`setInterval`, `setTimeout`) Not Cleared**
#### **Example: Memory Leak**
```jsx
useEffect(() => {
  setInterval(() => {
    console.log("Interval running...");
  }, 1000);

  // ❌ No cleanup function - interval keeps running after unmount
}, []);
```
#### **Fix: Clear Interval on Unmount**
```jsx
useEffect(() => {
  const interval = setInterval(() => {
    console.log("Interval running...");
  }, 1000);

  return () => clearInterval(interval);
}, []);
```

### ** References to DOM Elements**
If you create DOM elements manually and don't clean them up, they can **persist in memory**.

#### **Example: Memory Leak**
```jsx
function Component() {
  useEffect(() => {
    const div = document.createElement("div");
    document.body.appendChild(div);

    // ❌ No cleanup - div stays in memory
  }, []);
}
```
#### **Fix: Remove Created Elements**
```jsx
function Component() {
  useEffect(() => {
    const div = document.createElement("div");
    document.body.appendChild(div);

    return () => {
      document.body.removeChild(div);
    };
  }, []);
}
```

## **How to Detect Memory Leaks**
### **1️⃣ Chrome DevTools (Performance Tab)**
- Open **Chrome DevTools** → Go to **Memory** tab → Take a snapshot.
- Interact with your app and take another snapshot.
- If memory usage keeps increasing **without dropping**, you may have a memory leak.

### **2️⃣ Warnings in Console**
React shows warnings if you **try to update state on an unmounted component**.

```
Can't perform a React state update on an unmounted component.
```

### **3️⃣ React Developer Tools (Profiler)**
- Use the **React Profiler** to see if components are being unnecessarily retained in memory.

## **Key Takeaways**
✅ **Always clean up side effects in `useEffect` using a cleanup function.**  
✅ **Cancel API requests or ignore state updates if a component unmounts.**  
✅ **Remove event listeners and intervals when a component unmounts.**  
✅ **Use Chrome DevTools and React Profiler to detect memory leaks.**  

### Q : How garbage collection is done in reactJS?
A : ### **Garbage Collection in React (Minimal Explanation)**  

1. **React relies on JavaScript's garbage collector (GC)** to free up unused memory.  
2. **GC removes unreachable objects** using the **Mark & Sweep algorithm**.  
3. **Memory leaks happen when references persist** after a component unmounts.

### **Preventing Memory Leaks**  
- **Use cleanup functions** in `useEffect`.  
- **Remove unused state** when a component unmounts.  
- **Monitor memory** using Chrome DevTools (Memory tab).  

### Q : What is SyntheticEvent?
A : Certainly! In a simple way:

A SyntheticEvent in React is like a wrapper around real events (like clicks or keystrokes) that happen in a web browser. React uses it to make sure event handling works consistently across different browsers, making it easier for developers to work with events in their React components. It's like a standardized package for handling events, ensuring things work smoothly no matter which browser your app is running in.

### Q : What is Component?
A : In react, a component is reusable building block for creating UI.

### Q : What is pure component
A : A **PureComponent** in React is a type of component that implements **shouldComponentUpdate** with a shallow comparison of props and state. This means it prevents unnecessary re-renders by only updating if there are actual changes in its props or state.

Normally in React:
- When a parent re-renders, all child components re-render.

But with PureComponent:
- React checks if props or state actually changed.
- If no change, it skips rendering → improves performance.

### **Key Differences Between `PureComponent` and `Component`**
1. **Automatic Optimization:**  
   - `React.Component` re-renders on any state/prop update.  
   - `React.PureComponent` only re-renders when shallow comparison detects changes.
  
2. **Shallow Comparison:**  
   - It does a shallow comparison (`===`) on both **state** and **props** before deciding to re-render.

3. **Performance Boost:**  
   - In cases where re-renders are frequent and costly, `PureComponent` can improve performance.

### **Example**
```jsx
import React, { PureComponent } from "react";

class MyComponent extends PureComponent {
  state = { count: 0 };

  increment = () => {
    this.setState({ count: this.state.count + 1 });
  };

  render() {
    console.log("Rendered"); // Only renders if state/props actually change
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.increment}>Increment</button>
      </div>
    );
  }
}

export default MyComponent;
```
#### **When to Use `PureComponent`?**
- When working with **functional components**, `React.memo` is a better alternative.
- When props and state are **simple and immutable** (deeply nested objects may still cause unwanted re-renders).
- When performance optimization is necessary.

#### **When NOT to Use `PureComponent`?**
- If the state/props contain **complex nested objects**, as shallow comparison may not detect deep changes.
- If props/state are frequently updated but should always trigger a re-render.

### Q : What are the differences between functional and class components?
A : There are mainly two type

Before the introduction of Hooks in React, functional components were called stateless components and were behind class components on a feature basis. After the introduction of Hooks, functional components are equivalent to class components.

Although functional components are the new trend, the react team insists on keeping class components in React. Therefore, it is important to know how these components differ.

* Function Components: This is the simplest way to create a component. Those are pure JavaScript functions that accept props object as the first parameter and return React elements to render the output:
```
function card(props){
   return(
      <div className="main-container">
        <h2>Title of the card</h2>
      </div>
    )
}
//---- OR
const card = (props) =>{
    return(
      <div className="main-container">
        <h2>Title of the card</h2>
      </div>
    )
}
```

* Class Components: You can also use ES6 class to define a component. The above function component can be written as a class component:
```
 class Card extends React.Component{
  constructor(props){
     super(props);
   }
    render(){
      return(
        <div className="main-container">
          <h2>Title of the card</h2>
        </div>
      )
    }
   }
```

### Q : When to use a Class Component over a Function Component?
A : * If the component needs state or lifecycle methods then use class component otherwise use function component. However, from React 16.8 with the addition of Hooks, you could use state , lifecycle methods and other features that were only available in class component right in your function component. 
* So, it is always recommended to use Function components, unless you need a React functionality whose Function component equivalent is not present yet, like Error Boundaries.

### Q : What is the virtual DOM? How does react use the virtual DOM to render the UI?
A : As stated by the react team, virtual DOM is a concept where a virtual representation of the real DOM is kept inside the memory and is synced with the real DOM by a library such as ReactDOM.

The Virtual DOM (VDOM) is an in-memory representation of Real DOM. The representation of a UI is kept in memory and synced with the "real" DOM. It's a step that happens between the render function being called and the displaying of elements on the screen. This entire process is called reconciliation.

### Q : What is reconciliation?
A : When a component's props or state change, React decides whether an actual DOM update is necessary by comparing the newly returned element with the previously rendered one. When they are not equal, React will update the DOM. This process is called reconciliation.

### Q : What is state in React?  
A : **State** is an object that stores component-specific data that may change over the component's lifecycle. It is **private** and fully controlled by the component itself. To maintain simplicity, we should keep the state minimal and avoid unnecessary stateful components.  

State is similar to props but **cannot be accessed by other components unless explicitly passed**.  

Example: A `User` component with a `message` state:  
```jsx
class User extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      message: 'Welcome to React world'
    };
  }

  render() {
    return (
      <div>
        <h1>{this.state.message}</h1>
      </div>
    );
  }
}
```

### Q : What are props in React?  
A : **Props** (short for "properties") are used to pass data from a **parent** component to a **child** component. They act like function arguments and **cannot be modified by the receiving component**.  

The primary purpose of props in React:  
* Pass **custom data** to child components.  
* **Trigger state changes** in child components.  
* Used inside a component's `render()` method via `this.props.someProp`.  

### Q : What is the difference between state and props?  
A :  

| Feature  | State | Props |
|----------|-------|-------|
| **Definition** | Internal data storage for a component | External data passed from parent to child |
| **Mutability** | Can be changed using `setState()` | Immutable (cannot be modified by child) |
| **Accessibility** | Private to the component | Accessible by child components |
| **Usage** | Stores dynamic data | Used for communication between components |
| **Example Usage** | Form inputs, toggles, counters | Component customization, data passing |


### Q : How to update a property within an object using setState?
A : 
To update a property within an object using `setState`, always create a **new object** instead of mutating the existing one.  

### **For Class Components**
Use `setState` with the **spread operator (`...`)** to update a specific property while keeping the rest of the object unchanged.  

```jsx
this.setState((prevState) => ({
  user: {
    ...prevState.user, 
    age: 30, // Updating only the age property
  },
}));
```

---

### **For Functional Components (`useState`)**
Use the functional update form of `setState` to ensure you're working with the latest state.

```jsx
const [user, setUser] = useState({ name: "Alice", age: 25 });

const updateAge = () => {
  setUser((prevUser) => ({
    ...prevUser, 
    age: 30, // Updating only age
  }));
};
```

**❌ Avoid Mutating State Directly:**  
```jsx
user.age = 30; // ❌ This won't trigger re-render
setUser(user); // ❌ Still incorrect, state should be immutable
```

### **Key Takeaways**
✅ Always create a new object using `{ ...prevState }`  
✅ Use functional updates `setState((prev) => { ...prev })`  
✅ Never mutate state directly  

### Q : Why should we not update the state directly?
A :  you try to update the state directly then it won't re-render the component.

//Wrong
```
this.state.message = 'Hello world'
```
Instead use setState() method. It schedules an update to a component's state object. When state changes, the component responds by re-rendering.

//Correct
```
this.setState({ message: 'Hello World' })
```
Note: You can directly assign to the state object either in constructor or using latest javascript's class field declaration syntax.

### Q : What are the differences between controlled and uncontrolled components?
A : 
## Controlled vs Uncontrolled Components in React
These terms are mainly used with **form elements** like `input`, `textarea`, `select`.
---
# 1️⃣ Controlled Component
A **controlled component** is a form element whose **value is controlled by React state**.
React manages the data using `useState`.

### Example

```javascript
import React, { useState } from "react";

function App() {
  const [name, setName] = useState("");

  return (
    <input
      type="text"
      value={name}
      onChange={(e) => setName(e.target.value)}
    />
  );
}
```

### How it works
1. User types something
2. `onChange` fires
3. React updates state
4. State updates the input value

So **React controls the input**.

---

# 2️⃣ Uncontrolled Component
An **uncontrolled component** stores form data **inside the DOM itself**, not in React state.
We use **`useRef`** to read the value.

### Example

```javascript
import React, { useRef } from "react";

function App() {
  const inputRef = useRef();

  const handleClick = () => {
    alert(inputRef.current.value);
  };

  return (
    <>
      <input type="text" ref={inputRef} />
      <button onClick={handleClick}>Submit</button>
    </>
  );
}
```

### How it works
1. User types in input
2. Value stays in DOM
3. React reads value using `ref`

So **DOM controls the input**.
---
# Key Differences

| Controlled             | Uncontrolled      |
| ---------------------- | ----------------- |
| Managed by React state | Managed by DOM    |
| Uses `useState`        | Uses `useRef`     |
| More control           | Less control      |
| Easier validation      | Harder validation |

---
# Simple Interview Answer

> A controlled component is a form element whose value is controlled by React state, while an uncontrolled component stores its value in the DOM and is accessed using refs.
---
💡 **Real-world tip:**
Most React applications use **controlled components** because they make **validation, form handling, and state management easier**.
---

### Q : What are the lifecycle methods of React?
A : 
* componentWillMount
* componentDidMount
* componentWillReceiveProps
* shouldComponentUpdate
* componentWillUpdate
* componentDidUpdate
* componentWillUnmount

### Q : What is the purpose of callback function as an argument of setState()?
A : The callback function is invoked when setState finished and the component gets rendered. Since setState() is asynchronous the callback function is used for any post action.

Note: It is recommended to use lifecycle method rather than this callback function.
```
setState({ name: "John" }, () =>
  console.log("The name has updated and component re-rendered")
);
```

### Q : What is "key" prop and what is the benefit of using it in arrays of elements?
A : In React, the `key` prop is a special attribute that should be assigned to elements inside an array to help React identify which items have changed, been added, or been removed. When rendering a list of elements using the `map` function, each rendered element should have a unique `key` prop.

The `key` prop serves two primary purposes:

1. **Optimizing Reconciliation:** React uses the `key` prop to optimize the process of reconciling the virtual DOM with the actual DOM. When an array of elements is updated (e.g., elements are added, removed, or reordered), React can efficiently update only the elements that have changed by comparing their keys.

2. **Preserving Component State:** The `key` prop helps React maintain component state between renders. If the `key` of an element remains the same across renders, React can identify it as the same element, preserving its state. If the `key` changes, React treats it as a different element.

Here's an example of using the `key` prop when rendering a list of elements:

```jsx
const MyList = ({ items }) => {
  return (
    <ul>
      {items.map(item => (
        <li key={item.id}>{item.name}</li>
      ))}
    </ul>
  );
};

// Example usage:
const items = [
  { id: 1, name: 'Item 1' },
  { id: 2, name: 'Item 2' },
  { id: 3, name: 'Item 3' },
];

ReactDOM.render(<MyList items={items} />, document.getElementById('root'));
```
* It's important to note that the `key` should be unique among siblings but doesn't need to be globally unique. React uses the `key` prop to optimize the performance of updates within the same parent component. If the `key` prop is omitted, React may issue a warning, and it's generally good practice to provide a meaningful and stable `key` for each element in a list.

### Q : What are Higher-Order Components?
A : 
A higher-order component (HOC) is a function that takes a component and returns a new component. Basically, it's a pattern that is derived from React's compositional nature.

We call them pure components because they can accept any dynamically provided child component but they won't modify or copy any behavior from their input components.

const EnhancedComponent = higherOrderComponent(WrappedComponent)

```
import React from "react";

// HOC
function withMessage(Component) {
  return function () {
    return (
      <div>
        <h3>Welcome!</h3>
        <Component />
      </div>
    );
  };
}

// Normal component
function Hello() {
  return <h2>Hello Foram</h2>;
}

// Wrap component using HOC
const EnhancedHello = withMessage(Hello);

// App component
export default function App() {
  return (
    <div>
      <EnhancedHello />
    </div>
  );
}
```
HOC can be used for many use cases:
* Code reuse, logic and bootstrap abstraction.
* Render hijacking.
* State abstraction and manipulation.
* Props manipulation.

### Q : What are the rules that must be followed while using React Hooks?
A :
* React Hooks must be called only at the top level. It is not allowed to call them inside the nested functions, loops, or conditions.
* It is allowed to call the Hooks only from the React Function Components.

### Q : Name a few techniques to optimize React app performance.
A : Yes, there are several techniques you can employ to improve the performance of React.js applications:

1. **Code Splitting**: As mentioned earlier, code splitting helps in reducing the initial bundle size by loading only the necessary code for the current view, thus improving the load time.

2. **Memoization**: Use the `React.memo()` higher-order component or the `useMemo()` hook to memoize components or values that don't need to be recalculated on every render, improving rendering performance.

3. **Virtual DOM Optimization**: React's virtual DOM efficiently updates the actual DOM, but you can further optimize by minimizing the number of re-renders through techniques like shouldComponentUpdate lifecycle method, PureComponent, or using hooks like `useCallback()` to memoize event handlers.

4. **Optimized Rendering**: Use efficient rendering techniques like keys for lists, to enable React to identify which items have changed, thus reducing the number of re-renders.

5. **Bundle Size Optimization**: Minimize the size of your JavaScript bundle by using tools like Webpack or Rollup along with techniques like tree shaking, code splitting, and minimizing dependencies.

6. **Performance Profiling**: Use tools like React DevTools or browser developer tools to profile and identify performance bottlenecks. Optimize components or operations that are causing performance issues.

7. **Server-Side Rendering (SSR) or Static Site Generation (SSG)**: SSR and SSG can be used to pre-render React components on the server or at build time, respectively, improving initial load times and SEO performance.

8. **State Management Optimization**: Use efficient state management libraries like Redux or React Context API and ensure that state updates are batched where possible to minimize unnecessary re-renders.

9. **Bundle Compression and Gzip**: Compress your bundle using tools like Brotli or Gzip to reduce file sizes, resulting in faster downloads.

10. **Lazy Loading and Code Splitting for Images and Assets**: Use lazy loading and code splitting techniques not only for JavaScript but also for images and other assets to defer loading until they are needed.

* when you have too muchh data you can do pagination

* also in beginnnig of you project you can use webpack.

* Code splitting in React.js refers to a technique used to optimize the performance of web applications by breaking down the JavaScript codebase into smaller chunks, and loading them only when they are needed. This helps to reduce the initial bundle size of the application, making the initial page load faster and improving the overall user experience.

In React, code splitting can be achieved using dynamic imports, also known as lazy loading. With dynamic imports, you can import components or modules asynchronously, meaning they are fetched from the server only when they are required, typically triggered by user actions such as navigating to a specific route or interacting with a particular feature.

### Q : What is fragment in react?
A : In React, a fragment is a lightweight syntax that allows you to group multiple elements without adding an extra node to the DOM. Fragments are particularly useful when you need to return multiple elements from a component, and you don't want to introduce an additional parent node in the HTML structure.

* Fragments are a bit faster and use less memory by not creating an extra DOM node. This only has a real benefit on very large and deep trees.
* Some CSS mechanisms like Flexbox and CSS Grid have a special parent-child relationships, and adding divs in the middle makes it hard to keep the desired layout.
* The DOM Inspector is less cluttered.

```jsx
import React from 'react';

const MyComponent = () => {
  return (
    <>
      <h1>Hello</h1>
      <p>React Fragments</p>
    </>
  );
};
```

* In this example, `<>` and `</>` are shorthand syntax for a fragment. It's equivalent to using `<React.Fragment>` and `</React.Fragment>`. The elements inside the fragment are siblings and can be rendered without introducing an additional div or other container element to the DOM.

* Fragments help in keeping the HTML structure clean and avoiding unnecessary nesting, which can be beneficial for styling and layout purposes. They are especially handy when you need to return multiple elements from a component function without creating an artificial parent node in the rendered output.

### Q : Diff between all fregment

| Wrapper | Extra DOM Element? | Can Accept Attributes? | When to Use? |
|---------|------------------|-------------------|--------------|
| `<div>...</div>` | ✅ Yes | ✅ Yes | When you need a container for styling, layout, or applying CSS classes. |
| `<React.Fragment>...</React.Fragment>` | ❌ No | ✅ Yes | When you want to group elements without adding extra DOM nodes and need to use keys or attributes. |
| `<>...</>` (Shorthand) | ❌ No | ❌ No | When you want a cleaner syntax and don’t need attributes like `key`. |

This keeps it concise and clear. Let me know if you need tweaks! 🚀

### Q : Explain about types of Hooks in React.
A : 
* useState(): This functional component is used to set and retrieve the state.
* useEffect(): It enables for performing the side effects in the functional components.
* useContext(): It is used for creating common data that is to be accessed by the components hierarchy without having to pass the props down to each level.
* useRef() : It will permit creating a reference to the DOM element directly within the functional component.
* useLayoutEffect(): It is used for the reading layout from the DOM and re-rendering synchronously.
* useMemo() : This will be used for recomputing the memoized value when there is a change in one of the dependencies. This optimization will help for avoiding expensive calculations on each render.
* useCallback() : This is useful while passing callbacks into the optimized child components and depends on the equality of reference for the prevention of unneeded renders.

### Q : What is custom hooks and what is use?
A :
### **What is a Custom Hook?**  
A **Custom Hook** in React is a **JavaScript function** that starts with `use` and **encapsulates reusable logic** using other hooks.

### **Why Use Custom Hooks?**  
✅ **Reusability** – Avoid duplicating logic across components.  
✅ **Separation of Concerns** – Keep components clean and focused.  
✅ **Improved Readability** – Encapsulate complex logic.

---

### **Example: useFetch Hook**  
A custom hook to fetch data.  
```jsx
import { useState, useEffect } from "react";

const useFetch = (url) => {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch(url)
      .then((res) => res.json())
      .then((data) => setData(data));
  }, [url]);

  return data;
};

export default useFetch;
```
**Usage:**  
```jsx
const App = () => {
  const users = useFetch("https://api.example.com/users");
  return <pre>{JSON.stringify(users, null, 2)}</pre>;
};
```

### Q : what are the potential options for using useRef?
A : 
`useRef` is used to **persist values across renders** without causing re-renders.  

#### **1️⃣ Accessing & Manipulating DOM**  
Best for handling focus, animations, and scrolling.  
```jsx
const InputFocus = () => {
  const inputRef = useRef(null);

  return (
    <>
      <input ref={inputRef} />
      <button onClick={() => inputRef.current.focus()}>Focus</button>
    </>
  );
};
```

#### **2️⃣ Storing Values Without Re-Renders**  
Keeps a value between renders without triggering updates.  
```jsx
const Counter = () => {
  const count = useRef(0);

  return <button onClick={() => count.current++}>Count: {count.current}</button>;
};
```

#### **3️⃣ Tracking Previous State or Props**  
Stores the previous value to compare changes.  
```jsx
const PreviousValue = ({ count }) => {
  const prevCount = useRef(count);

  useEffect(() => { prevCount.current = count; });

  return <p>Now: {count}, Before: {prevCount.current}</p>;
};
```

#### **4️⃣ Handling Timers & Cleanup**  
Prevents memory leaks in `setTimeout` or `setInterval`.  
```jsx
const Timer = () => {
  const timerRef = useRef(null);

  useEffect(() => {
    timerRef.current = setInterval(() => console.log("Tick"), 1000);
    return () => clearInterval(timerRef.current); // Cleanup
  }, []);

  return <p>Running...</p>;
};
```

#### **5️⃣ Integrating with Third-Party Libraries**  
Passes a direct reference to external libraries like **Chart.js, GSAP**.  
```jsx
const Canvas = () => {
  const canvasRef = useRef(null);

  useEffect(() => {
    const ctx = canvasRef.current.getContext("2d");
    ctx.fillStyle = "red";
    ctx.fillRect(0, 0, 100, 100);
  }, []);

  return <canvas ref={canvasRef} width="200" height="200"></canvas>;
};
```

### **Summary: When to Use `useRef`?**
| Use Case | Why? |
|----------|------|
| **Accessing DOM elements** | Manipulate without re-render |
| **Storing values** | Persist values without triggering updates |
| **Tracking previous state/props** | Compare past & current values |
| **Handling timers** | Avoid memory leaks in intervals |
| **Third-party libraries** | Pass refs for external integrations |

### Q : Diff between memo, usememo and usecallback
A :
Remember this sentence:
**"memo → component, useMemo → value, useCallback → function"**
---
### React.memo
Used for **components**
It stops a **component** from re-rendering if props didn't change.

```javascript
const Child = React.memo((props) => {
  return <h2>{props.name}</h2>;
});
```
**Remembers component render**
---
### useMemo
Used for **values / calculations**
It **stores a calculated value** so React doesn't calculate again.
```javascript
const result = useMemo(() => {
  return num * 2;
}, [num]);
```
**Remembers value**
---
### useCallback
Used for **functions**
It **stores a function** so it is not recreated on every render.
```javascript
const handleClick = useCallback(() => {
  console.log("clicked");
}, []);
```
**Remembers function**
---
# ⚡ Super Easy Table
| Hook        | Remembers |
| ----------- | --------- |
| React.memo  | Component |
| useMemo     | Value     |
| useCallback | Function  |
---
### 5-Second Interview Answer
**React.memo** → prevents component re-render
**useMemo** → memoizes calculated values
**useCallback** → memoizes functions
---
**One last simple way to remember**
```
memo → component
useMemo → memory of value
useCallback → memory of function
```
---
In summary, useMemo is used to memoize values, while useCallback is specifically designed for memoizing callback functions. Both are performance optimization tools, and they help in avoiding unnecessary recalculations or re-renders in React components. Use useMemo when dealing with memoizing values, and use useCallback when dealing with memoizing callback functions.

### Q : what is life cycle equivalent in react function component?
A :
In React **functional components**, lifecycle methods are replaced by **hooks** like `useEffect`. Here's how lifecycle methods from class components map to functional components:

## **Lifecycle Equivalents in Functional Components**

| **Class Component Lifecycle**     | **Functional Component Equivalent (Hooks)** |
|-----------------------------------|---------------------------------------------|
| **`componentDidMount`** <br> (Runs once when the component is mounted) | `useEffect(() => {...}, [])` |
| **`componentDidUpdate`** <br> (Runs when props/state change) | `useEffect(() => {...}, [dependencies])` |
| **`componentWillUnmount`** <br> (Runs before the component is unmounted) | `useEffect(() => { return () => {...} }, [])` |
| **`shouldComponentUpdate`** <br> (Decides if re-render is needed) | `React.memo(Component)` or `useMemo/useCallback` |
| **`componentWillReceiveProps`** <br> (Runs when props change) | `useEffect(() => {...}, [prop])` |
| **`componentWillMount`** *(deprecated)* | Not needed, initialization happens inside function body |

## **Example of Lifecycle Equivalents Using Hooks**
```jsx
import React, { useState, useEffect } from "react";

const MyComponent = ({ count }) => {
  const [data, setData] = useState(null);

  // Equivalent to componentDidMount
  useEffect(() => {
    console.log("Component mounted");
    fetchData();

    // Equivalent to componentWillUnmount (cleanup)
    return () => {
      console.log("Component unmounted");
    };
  }, []);

  // Equivalent to componentDidUpdate (runs when count changes)
  useEffect(() => {
    console.log("Count changed:", count);
  }, [count]);

  return <h1>Count: {count}</h1>;
};

export default MyComponent;
```

### Q : How to do clean up functional component in react with one example and why it is needed there?
A :
In React functional components, **cleanup** is done using the **cleanup function inside `useEffect`**. The cleanup function runs **when the component unmounts** or **before the effect runs again** (if dependencies change).  

### **Why is Cleanup Needed?**
1. **Prevent Memory Leaks** → Cleanup prevents unwanted listeners, timers, or subscriptions from persisting after the component unmounts.
2. **Avoid Side Effects** → Stops unnecessary API calls, event listeners, or intervals that may cause unexpected behavior.
3. **Improve Performance** → Ensures resources are freed when a component is no longer needed.

Absolutely! Let's break down how `useEffect` works and why cleanup is important in this case.

### **Understanding `useEffect` and Cleanup:**
`useEffect` in React is a hook that allows you to run side effects in function components. It runs after the render, which makes it perfect for tasks like:
- Fetching data from an API
- Subscribing to events
- Updating the document title

The **cleanup function** inside `useEffect` is used to **clean up side effects** when the component unmounts or before the effect runs again. This is especially important for scenarios where resources need to be freed (like network requests or subscriptions).

### Q : What are some common usage and pitfalls of useEffect
A :
### **What is `useEffect`?**  
`useEffect` is a **React Hook** used in functional components to handle **side effects** such as:  
- Fetching data from an API  
- Subscribing to events or WebSockets  
- Manipulating the DOM  
- Setting up timers or intervals  

It runs **after the component renders** and can be configured to run under different conditions.

## ✅ **Usage of `useEffect`**  
### **1. Run on Every Render (No Dependencies)**
```jsx
useEffect(() => {
  console.log("Component rendered!");
});
```
- This runs **after every render** (initial + re-renders).  
- **Common use case:** Debugging or updating document title dynamically.

### **2. Run Once (On Mount)**
```jsx
useEffect(() => {
  console.log("Component mounted!");

  return () => console.log("Cleanup on unmount!");
}, []); // Empty dependency array
```
- Runs **only once** when the component mounts.  
- **Cleanup function** runs when the component **unmounts**.  
- **Common use case:**  
  - Adding/removing event listeners  
  - Initial API call  

### **3. Run When Dependencies Change**
```jsx
const [count, setCount] = useState(0);

useEffect(() => {
  console.log(`Count changed to: ${count}`);
}, [count]); // Runs when `count` changes
```
- Runs when **dependencies change** (`count` in this case).  
- **Common use case:**  
  - Fetching new data when user input changes.  

### **4. Fetching Data with Cleanup**
```jsx
useEffect(() => {
  const controller = new AbortController(); // Helps cancel request on unmount
  fetch("https://api.example.com/data", { signal: controller.signal });

  return () => controller.abort(); // Cleanup API call
}, []);
```
- Ensures **API calls don’t continue** after the component unmounts.

## ❌ **Common Pitfalls of `useEffect`**
### **1. Infinite Re-renders (Missing Dependency Array)**
```jsx
useEffect(() => {
  setCount(count + 1); // ❌ Causes an infinite loop
});
```
- **Fix:** Add dependencies to prevent repeated execution.

### **2. Unnecessary Re-renders (Too Many Dependencies)**
```jsx
useEffect(() => {
  console.log("Re-run effect!");
}, [user, posts, comments]); // ❌ Runs even if only one changes
```
- **Fix:** Minimize dependencies by using selective values.

### **3. Memory Leaks (Not Cleaning Up)**
```jsx
useEffect(() => {
  window.addEventListener("resize", handleResize); // ❌ Not removed on unmount
}, []);
```
- **Fix:** Always **clean up** listeners in the return function:
  ```jsx
  useEffect(() => {
    window.addEventListener("resize", handleResize);

    return () => window.removeEventListener("resize", handleResize);
  }, []);
  ```

## **Final Takeaways**
✅ Use `useEffect` for **side effects** like data fetching and event handling.  
✅ Always **add dependencies** carefully to avoid infinite loops.  
✅ **Cleanup effects** when needed to **prevent memory leaks**.  
✅ Use an **empty array (`[]`)** if you only want it to run on mount/unmount.  

### Q : What are some common pitfalls when doing data fetching?
A : ### 1️⃣ **Updating State After Unmounting**  
- If a component unmounts before a fetch completes, updating the state can cause errors.  
- **Fix:** Use `useEffect` cleanup or check `isMounted`.  
  ```js
  useEffect(() => {
    let isMounted = true;
    fetchData().then((data) => {
      if (isMounted) setData(data);
    });
    return () => { isMounted = false; };
  }, []);
  ```

### 2️⃣ **Not Handling Errors Properly**  
- Network failures, API errors, or invalid responses can cause crashes.  
- **Fix:** Always use `try-catch` or `.catch()` for error handling.  
  ```js
  fetchData().catch((error) => console.error("Fetch failed:", error));
  ```

### 3️⃣ **Unnecessary Re-fetching**  
- Fetching inside `useEffect` without dependencies causes unnecessary API calls.  
- **Fix:** Pass an empty dependency array (`[]`) or memoize values.  
  ```js
  useEffect(() => {
    fetchData();
  }, []); // Fetch only once
  ```

### 4️⃣ **Race Conditions**  
- Multiple fetches may return in the wrong order, overwriting correct data.  
- **Fix:** Use **aborting requests** with `AbortController`.  
  ```js
  useEffect(() => {
    const controller = new AbortController();
    fetchData({ signal: controller.signal });

    return () => controller.abort();
  }, []);
  ```

### 5️⃣ **Blocking UI During Fetching**  
- Not handling loading states can make UI feel unresponsive.  
- **Fix:** Use a `loading` state.  
  ```js
  const [loading, setLoading] = useState(true);
  useEffect(() => {
    fetchData().then(() => setLoading(false));
  }, []);
  ```

### 6️⃣ **Fetching Inside Render**  
- Calling fetch directly inside a component body causes infinite loops.  
- **Fix:** Always fetch inside `useEffect` or lifecycle methods.  

### 7️⃣ **Memory Leaks Due to Unused Event Listeners**  
- Forgetting to clean up event listeners in useEffect can cause memory leaks.  
- **Fix:** Use `return` in `useEffect` to clean up listeners.  

### Q : What is context?
A : Context provides a way to pass data through the component tree without having to pass props down manually at every level.

For example, authenticated users, locale preferences, UI themes need to be accessed in the application by many components.
```
const { Provider, Consumer } = React.createContext(defaultValue);
```
### Q : why a component is sluggish in between renders
A : 
A component can feel **sluggish between renders** due to several reasons:  

### **1️⃣ Excessive Re-Renders**
- **Cause**: Unnecessary state updates or parent re-renders.  
- **Fix**: Use `React.memo` to prevent re-renders when props haven't changed.  
  ```jsx
  const MyComponent = React.memo(({ data }) => <div>{data}</div>);
  ```

### **2️⃣ Expensive Computations in Render**
- **Cause**: Running heavy calculations inside the render function.  
- **Fix**: Use `useMemo` to cache expensive calculations.  
  ```jsx
  const processedData = useMemo(() => heavyComputation(data), [data]);
  ```

### **3️⃣ Unoptimized State Updates**
- **Cause**: Updating state in a way that triggers unnecessary renders.  
- **Fix**: Use functional updates in `useState` if the new state depends on the previous state.  
  ```jsx
  setCount((prev) => prev + 1);
  ```

### **4️⃣ Overuse of useEffect**
- **Cause**: Running expensive tasks on every render.  
- **Fix**: Add dependencies carefully to avoid unnecessary executions.  
  ```jsx
  useEffect(() => {
    fetchData();
  }, []); // Runs only once
  ```

### **5️⃣ Large Component Trees**
- **Cause**: Too many components re-rendering unnecessarily.  
- **Fix**: Split components into smaller, memoized pieces.  

### **6️⃣ Unoptimized List Rendering**
- **Cause**: Re-rendering the whole list when only one item changes.  
- **Fix**: Use `key` properly and consider virtualization (`react-window`).  
  ```jsx
  {items.map((item) => (
    <ListItem key={item.id} data={item} />
  ))}
  ```

### **7️⃣ Blocking the Main Thread**
- **Cause**: Running synchronous code that blocks rendering.  
- **Fix**: Use Web Workers or `useTransition` for smoother updates.  
  ```jsx
  const [isPending, startTransition] = useTransition();
  startTransition(() => setState(newData));
  ```

### **💡 Quick Fixes**
✅ Use **React.memo** for pure components.  
✅ Use **useMemo** and **useCallback** for expensive operations.  
✅ Optimize **list rendering** with `key`.  
✅ Avoid **unnecessary state updates** and **useEffect misuse**.  
✅ Use **Web Workers** or `useTransition` for heavy computations.  

### Q : What would be the common mistake of function being called every time the component renders?
You need to make sure that function is not being called while passing the function as a parameter.
```
render() {
  // Wrong: handleClick is called instead of passed as a reference!
  return <button onClick={this.handleClick()}>{'Click Me'}</button>
}
```
Instead, pass the function itself without parenthesis:
```
render() {
  // Correct: handleClick is passed as a reference!
  return <button onClick={this.handleClick}>{'Click Me'}</button>
}
```

### Q : What are error boundaries in React v16?
A : Error boundaries are components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI instead of the component tree that crashed.

A class component becomes an error boundary if it defines a new lifecycle method called componentDidCatch(error, info) or static getDerivedStateFromError().

### Q : How to use innerHTML in React?
A : The dangerouslySetInnerHTML attribute is React's replacement for using innerHTML in the browser DOM. Just like innerHTML, it is risky to use this attribute considering cross-site scripting (XSS) attacks. You just need to pass a __html object as key and HTML text as value.

In this example MyComponent uses dangerouslySetInnerHTML attribute for setting HTML markup:
```
function createMarkup() {
  return { __html: "First &middot; Second" };
}

function MyComponent() {
  return <div dangerouslySetInnerHTML={createMarkup()} />;
}
```

### Q : What happens with a component when it receives new props?
A :
https://www.joshwcomeau.com/react/why-react-re-renders/#its-not-about-the-props-2
https://blog.logrocket.com/how-when-to-force-react-component-re-render#incorrectly-updated-props-without-state-change

### **Does a Component Always Re-Render When Props Change?**  

**Not exactly!** A component **does not always re-render** just because props change. Instead, it follows these behaviors:  

### **1️⃣ When Do Components Re-Render?**
🔹 **Functional Components**  
- A component **re-renders when:**
  1. Its **state** changes (`useState` update).
  2. Its **props** change (only if the new prop is different from the previous one).
  3. Its **parent re-renders** (even if the props stay the same).  

🔹 **Class Components**  
- A class component **re-renders when:**
  1. **State changes** via `this.setState()`.
  2. **New props are received**.
  3. **Its parent re-renders** (unless `shouldComponentUpdate` prevents it).  

### **2️⃣ Does a Component Re-Render If Only Props Change?**  
✅ **Yes, if the new prop value is different from the previous one.**  
❌ **No, if the new prop is the same as the previous one.**  

📌 **Example (No Re-Render if Props Are the Same)**  
```jsx
const Parent = () => {
  const [count, setCount] = useState(0);
  return (
    <>
      <button onClick={() => setCount(count)}>Update Parent</button>
      <Child message="Hello" />
    </>
  );
};

const Child = React.memo(({ message }) => {
  console.log("Child rendered");
  return <h1>{message}</h1>;
});
```
👉 Here, even though `Parent` re-renders, `Child` **does not re-render** because `message` ("Hello") remains the same.

### **3️⃣ Does a Component Re-Render If Only the Parent Re-Renders?**
✅ **Yes, by default, child components re-render when the parent re-renders—even if props don’t change.**  
❌ **No, if wrapped in `React.memo` (functional components) or `shouldComponentUpdate` (class components).**  

📌 **Example (Preventing Unnecessary Re-Renders)**  
```jsx
const Parent = () => {
  const [count, setCount] = useState(0);

  return (
    <>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <MemoizedChild message="Hello" />
    </>
  );
};

const MemoizedChild = React.memo(({ message }) => {
  console.log("Child rendered");
  return <h1>{message}</h1>;
});
```
👉 **Now, even if `Parent` re-renders, `Child` does not,** because `React.memo` prevents re-rendering when props remain the same.

### **4️⃣ Summary 🚀**
✔ **Props Change → Component Re-Renders (Only if the new prop value is different).**  
✔ **Parent Re-Renders → Child Re-Renders (Even if props don’t change).**  
✔ **Use `React.memo` or `shouldComponentUpdate` to prevent unnecessary re-renders.**  

Would you like a deep dive into how **React’s reconciliation process** handles re-renders? 🚀

### **1️⃣ Default Behavior: Component Re-Renders**  
- If the **new props** are different from the **previous ones**, React **triggers a re-render** of the component.  
- This applies to both **functional** and **class components**.

### **2️⃣ React Functional Components with `useEffect`**  
- If a component relies on **props** inside a `useEffect` dependency array, it will **run again** when props change.  
- Example:  
  ```jsx
  import React, { useEffect } from "react";

  const Child = ({ message }) => {
    useEffect(() => {
      console.log("Message prop changed:", message);
    }, [message]); // Runs when `message` prop changes

    return <h1>{message}</h1>;
  };
  ```

### **3️⃣ React Class Components with `componentDidUpdate`**  
- In class components, `componentDidUpdate(prevProps)` can detect prop changes.  
- Example:  
  ```jsx
  class Child extends React.Component {
    componentDidUpdate(prevProps) {
      if (prevProps.message !== this.props.message) {
        console.log("Message prop changed:", this.props.message);
      }
    }

    render() {
      return <h1>{this.props.message}</h1>;
    }
  }
  ```

### **4️⃣ `shouldComponentUpdate` (Class Components) & `React.memo` (Functional Components) for Optimization**  
- **By default, a component always re-renders when it receives new props.**  
- To **prevent unnecessary re-renders**, use:  
  - **`shouldComponentUpdate`** in class components.  
  - **`React.memo`** in functional components.  

#### ✅ Using `React.memo` (Functional Components)
```jsx
const Child = React.memo(({ message }) => {
  console.log("Child component rendered");
  return <h1>{message}</h1>;
});
```
> **Now, `Child` will only re-render if `message` actually changes.**  

#### ✅ Using `shouldComponentUpdate` (Class Components)
```jsx
class Child extends React.Component {
  shouldComponentUpdate(nextProps) {
    return nextProps.message !== this.props.message;
  }

  render() {
    return <h1>{this.props.message}</h1>;
  }
}
```
> **Prevents re-rendering if `message` stays the same.**  

### **5️⃣ What If Props Don't Change?**
- If **new props are identical** to the previous ones:
  - **No re-render happens.**  
  - If **React.memo** or **shouldComponentUpdate** is used, React skips rendering.  

### **Summary 🚀**  
✔️ **New props → Component re-renders** (default behavior).  
✔️ **Use `useEffect([prop])`** to react to prop changes in functional components.  
✔️ **Use `componentDidUpdate(prevProps)`** to detect changes in class components.  
✔️ **Optimize re-renders** with `React.memo` (functional) & `shouldComponentUpdate` (class).  

### Q : How to do error handling in react app
A : Handling errors in a React application involves implementing mechanisms to gracefully handle unexpected issues, such as runtime errors, API failures, or asynchronous operations. Here are some common approaches for error handling in a React app:

1. **Using `try` and `catch` for Asynchronous Code:**
   - Wrap asynchronous code (e.g., API calls, promises) in a `try...catch` block to capture and handle errors.

    ```javascript
    async function fetchData() {
      try {
        const response = await fetch('https://api.example.com/data');
        const data = await response.json();
        // Process the data
      } catch (error) {
        // Handle errors (e.g., log, display a user-friendly message)
        console.error('Error fetching data:', error.message);
      }
    }
    ```

2. **Error Boundaries:**
   - Use React Error Boundaries to catch JavaScript errors that occur anywhere in a component tree. Error boundaries are special components that can catch errors during rendering, in lifecycle methods, and in constructors.

    ```javascript
    class ErrorBoundary extends React.Component {
      constructor(props) {
        super(props);
        this.state = { hasError: false };
      }

      static getDerivedStateFromError(error) {
        return { hasError: true };
      }

      componentDidCatch(error, errorInfo) {
        // Log the error or send it to an error tracking service
        console.error('Error caught by error boundary:', error, errorInfo);
      }

      render() {
        if (this.state.hasError) {
          return <p>Something went wrong!</p>;
        }
        return this.props.children;
      }
    }
    ```

   - Wrap components or parts of the application tree with the `ErrorBoundary` component.

    ```javascript
    <ErrorBoundary>
      <MyComponent />
    </ErrorBoundary>
    ```

3. **Global Error Handling:**
   - Use `window.onerror` or `window.addEventListener('error')` to capture global errors.

    ```javascript
    window.addEventListener('error', (event) => {
      // Handle the error
      console.error('Global error:', event.error);
    });
    ```

4. **Axios Interceptors for API Calls:**
   - If using Axios for HTTP requests, utilize interceptors to handle errors globally.

    ```javascript
    axios.interceptors.response.use(
      (response) => response,
      (error) => {
        // Handle API response errors
        console.error('API error:', error.message);
        return Promise.reject(error);
      }
    );
    ```

5. **Displaying User-Friendly Messages:**
   - Present users with meaningful error messages or fallback UIs to communicate issues without revealing too much technical detail.

    ```javascript
    function MyComponent() {
      const [data, setData] = useState(null);
      const [error, setError] = useState(null);

      useEffect(() => {
        fetchData()
          .then((result) => setData(result))
          .catch((error) => setError('Error fetching data.'));
      }, []);

      if (error) {
        return <p>{error}</p>;
      }

      // Render component based on the fetched data
      return (
        <div>
          {/* Render component content */}
        </div>
      );
    }
    ```

Remember to tailor your error-handling strategy to the specific needs and characteristics of your application. Strive to provide a good user experience while also capturing relevant information for debugging during development.

## React Router

### Q : What is React Router?
A : React Router is a powerful routing library built on top of React that helps you add new screens and flows to your application incredibly quickly, all while keeping the URL in sync with what's being displayed on the page.

### Q : What are the <Router> components of React Router v4?
A : React Router v4 provides below 3 <Router> components:
*  BrowserRouter
*  HashRouter
*  MemoryRouter
The above components will create browser, hash, and memory history instances. React Router v4 makes the properties and methods of the history instance associated with your router available through the context in the router object.

### Q : What is the purpose of push() and replace() methods of history?
A : A history instance has two methods for navigation purpose.
* push()
* replace()
If you think of the history as an array of visited locations, push() will add a new location to the array and replace() will replace the current location in the array with the new one.

### Q : How to implement default or NotFound page?
A : 
```
<Switch>
  <Route exact path="/" component={Home} />
  <Route path="/user" component={User} />
  <Route component={NotFound} />
</Switch>
```
-----
```
import React from "react";
import ReactDOM from "react-dom";
//import { Route } from "react-router";
import { BrowserRouter, Routes, Route } from "react-router-dom";

import Login from "./Login";
import Register from "./Register";
import Dashboard from "./Dashboard";
import "./Login.css";

ReactDOM.render(
  <BrowserRouter>
    <Routes>
      <Route path="/" element={<Login />} />
      <Route path="/register" element={<Register />} />
      <Route path="/dashboard" element={<Dashboard />} />
    </Routes>
  </BrowserRouter>,
  document.getElementById("root")
);
```

## React Redux

### Q : What is flux
A : Flux is an architectural pattern developed by Facebook for managing state in web applications, particularly in conjunction with React. It introduces a unidirectional data flow, involving actions, a dispatcher, stores, and views (React components), to provide a structured and scalable approach to state management. The goal is to make it easier to handle complex state logic and maintainable user interfaces in large applications. While Flux itself is not a library or framework, it has influenced the design of state management libraries such as Redux.

### Q : What is Redux?
A : Redux is a predictable state container for JavaScript apps based on the Flux design pattern. Redux can be used together with React, or with any other view library. It is tiny (about 2kB) and has no dependencies.

* Action Creator ====>     Action    ====> Dispatch Action ====>     Reducer    ====> Central store
Compare to ticket booking below
*      You       ====> Booking Form  ====>  Submit Foram   ====> Ticket Counter ====> Railway Central Store

Redux is a predictable state container for JavaScript applications, commonly used with React for managing the state of applications in a more organized and scalable way. It follows the principles of the Flux architecture but introduces some key concepts and patterns that simplify state management.

### Key Concepts in Redux:

1. **Store:** The store is a single source of truth for the state of the entire application. It holds the current state tree and allows access to it. State in a Redux store is read-only, and any changes are made by dispatching actions.

2. **Actions:** Actions are plain JavaScript objects that describe an event or change in the application. They are the only way to modify the state in a Redux application. Actions must have a `type` property indicating the type of action being performed.

   Example:
   ```javascript
   {
     type: 'INCREMENT',
     payload: 1
   }
   ```

3. **Reducers:** Reducers are pure functions that specify how the state changes in response to an action. They take the current state and an action as arguments and return the next state. Reducers should not have side effects and should not modify the existing state; they create and return a new state.

   Example:
   ```javascript
   const counterReducer = (state = 0, action) => {
     switch (action.type) {
       case 'INCREMENT':
         return state + action.payload;
       default:
         return state;
     }
   };
   ```

4. **Dispatch:** The `dispatch` function is used to dispatch actions to the Redux store. When an action is dispatched, it triggers the execution of reducers, leading to a change in the state.

   Example:
   ```javascript
   store.dispatch({ type: 'INCREMENT', payload: 1 });
   ```

5. **Selectors:** Selectors are functions used to extract specific pieces of data from the state. They help in accessing and deriving data from the store without directly interacting with its structure.

   Example:
   ```javascript
   const getCounterValue = state => state.counter;
   ```

### Example Redux Setup:

```javascript
// store.js
import { createStore } from 'redux';
import rootReducer from './reducers'; // Combined reducers

const store = createStore(rootReducer);

export default store;
```

```javascript
// actions.js
export const increment = (amount) => ({
  type: 'INCREMENT',
  payload: amount
});
```

```javascript
// reducers.js
const counterReducer = (state = 0, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return state + action.payload;
    default:
      return state;
  }
};

// Combine reducers if needed
const rootReducer = combineReducers({
  counter: counterReducer,
  // other reducers...
});

export default rootReducer;
```

```javascript
// Component using Redux
import React from 'react';
import { useDispatch, useSelector } from 'react-redux';
import { increment } from './actions';

const MyComponent = () => {
  const counter = useSelector(state => state.counter);
  const dispatch = useDispatch();

  const handleIncrement = () => {
    dispatch(increment(1));
  };

  return (
    <div>
      <p>Counter: {counter}</p>
      <button onClick={handleIncrement}>Increment</button>
    </div>
  );
};
```

In this example, Redux is set up with a store, actions, reducers, and a React component that uses the `useSelector` and `useDispatch` hooks to interact with the Redux store. The state of the application is centralized in the Redux store, and changes are made through dispatched actions.

### Q : What is middleware in redux?
A : Let's create a simple middleware that logs each action dispatched in Redux along with the current state before and after the action is processed by the reducers. This will help us understand how middleware works in Redux.

Here's the middleware:

```javascript
const loggingMiddleware = store => next => action => {
  // Log the current state before the action is processed
  console.log('Current State:', store.getState());

  // Log the action being dispatched
  console.log('Dispatching Action:', action);

  // Call the next middleware in the chain or the dispatch function if this is the last middleware
  const result = next(action);

  // Log the new state after the action is processed by the reducers
  console.log('New State:', store.getState());

  // Return the result of calling the next middleware or the dispatch function
  return result;
};
```

Now, let's apply this middleware when creating the Redux store:

```javascript
import { createStore, applyMiddleware } from 'redux';
import rootReducer from './reducers'; // Assuming you have a root reducer

const store = createStore(
  rootReducer, // Your root reducer
  applyMiddleware(loggingMiddleware) // Apply loggingMiddleware
);
```

Here's what the middleware does:

1. It receives the `store` as an argument in its outer function, which represents the Redux store.
2. It returns another function that receives `next` as an argument. `next` is a reference to the next middleware in the chain or the dispatch function if there's no middleware left.
3. Inside the innermost function, it receives `action`, which is the action being dispatched.
4. It logs the current state before the action is processed.
5. It logs the action being dispatched.
6. It calls the `next` function with the `action`, which either passes the action to the next middleware or to the reducers.
7. After the action is processed by the reducers, it logs the new state.
8. It returns the result of calling the `next` function.

By applying this middleware, every action dispatched in your Redux application will be logged to the console along with the current and new state. This helps in debugging and understanding how actions affect the application state.

### Q : What are the core principles of Redux?
A : Redux follows three fundamental principles:

* Single source of truth: The state of your whole application is stored in an object tree within a single store. The single state tree makes it easier to keep track of changes over time and debug or inspect the application.

* State is read-only: The only way to change the state is to emit an action, an object describing what happened. This ensures that neither the views nor the network callbacks will ever write directly to the state.

* Changes are made with pure functions: To specify how the state tree is transformed by actions, you write reducers. Reducers are just pure functions that take the previous state and an action as parameters, and return the next state.

### Q : How to access Redux store outside a component?
A : You just need to export the store from the module where it created with createStore(). Also, it shouldn't pollute the global window object.
```
store = createStore(myReducer);
export default store;
```

### Q : What is the difference between React context and React Redux?
A : You can use Context in your application directly and is going to be great for passing down data to deeply nested components which what it was designed for.React Context is a React feature for sharing data across components in a component tree. It's flexible and suitable for scenarios where prop drilling becomes inconvenient.

Whereas Redux is much more powerful and provides a large number of features that the Context API doesn't provide. Also, React Redux uses context internally but it doesn't expose this fact in the public API. React Redux is a state management library specifically designed for managing complex state logic in React applications, following the Flux architecture principles. It provides a predictable and centralized way to handle application state.

### Q : What are Redux selectors and why to use them?
A : Selectors are functions that take Redux state as an argument and return some data to pass to the component.

For example, to get user details from the state:
```
const getUserData = (state) => state.user.data;
```
These selectors have two main benefits,

The selector can compute derived data, allowing Redux to store the minimal possible state
The selector is not recomputed unless one of its arguments changes

## Server Side rendering VS. Client Side Rendering
Here's a simplified comparison between Server-Side Rendering (SSR) and Client-Side Rendering (CSR):

| Feature                | Server-Side Rendering (SSR)                  | Client-Side Rendering (CSR)              |
|------------------------|----------------------------------------------|------------------------------------------|
| Where rendering happens| Rendering happens on the server.             | Rendering happens in the browser.        |
| Initial load           | Initial page loads faster.                   | Initial page load might be slower.       |
| Search engine indexing | Better for SEO.                              | Can be challenging for SEO.              |
| Server load            | Higher server load as it generates HTML.     | Lower server load, as it serves files.   |
| Development            | Can be more complex, especially for large apps.| Often simpler, focusing on client-side logic. |

In simple terms, with Server-Side Rendering, the server prepares the webpage before sending it to the user's browser, making the initial load faster and better for search engines. Client-Side Rendering, on the other hand, sends a basic webpage to the browser, which then uses JavaScript to load and display content, potentially making the initial load slower, but offering more dynamic and interactive experiences once loaded.

### Q : HOw to do Caching in react api call - This one i have removed can be checked upon latter
URL for ALL question :https://codeinterview.io/blog/reactjs-coding-interview-questions/

### Q : What is deduping and what is caching, retries and deduping in react?
A : 
### **Deduping in React**
Deduping (de-duplicating) in React refers to avoiding duplicate API calls for the same data. When multiple components request the same data, a deduplication strategy ensures that only a single request is sent to the backend, and all components use the same response.

For example, if two components fetch user details at the same time, deduping prevents sending two separate requests. Instead, it reuses the first request’s response for both components.

**Common Deduping Strategies:**
1. **Caching**: Store the response in memory and serve it if another request is made within a short time.
2. **Promise Tracking**: Track ongoing requests and return the same promise to multiple components instead of triggering duplicate requests.

### **Caching, Retries, and Deduping in React**
These are strategies used by libraries like **React Query, SWR, and Apollo Client** to optimize API calls.

1. **Caching**: Stores API responses in memory so that repeated requests within a given time frame return cached data instead of making a network call.
   
   **Example (SWR Caching)**:
   ```js
   import useSWR from 'swr';

   const fetcher = (url) => fetch(url).then((res) => res.json());

   function UserProfile() {
     const { data, error } = useSWR('/api/user', fetcher);
   
     if (error) return <div>Error loading user</div>;
     if (!data) return <div>Loading...</div>;
   
     return <div>{data.name}</div>;
   }
   ```
   - If another component requests `'/api/user'`, the cached response is used.
   - If the cache expires, a new request is sent.

2. **Retries**: If an API request fails (due to network issues or a temporary server error), the request is retried automatically before showing an error.
   
   **Example (React Query with Retries)**:
   ```js
   import { useQuery } from '@tanstack/react-query';

   const fetchUser = async () => {
     const response = await fetch('/api/user');
     if (!response.ok) throw new Error('Network error');
     return response.json();
   };

   function UserProfile() {
     const { data, error, isLoading } = useQuery({
       queryKey: ['user'],
       queryFn: fetchUser,
       retry: 3, // Retry up to 3 times
     });

     if (isLoading) return <div>Loading...</div>;
     if (error) return <div>Error loading user</div>;

     return <div>{data.name}</div>;
   }
   ```
   - If `fetchUser` fails, it will retry up to 3 times before showing an error.

3. **Deduping**: Ensures that multiple identical API calls made in a short period only trigger a **single** request.
   
   **Example (SWR Deduping)**:
   ```js
   import useSWR from 'swr';

   function ComponentA() {
     const { data } = useSWR('/api/data', fetcher);
     return <div>Data: {data}</div>;
   }

   function ComponentB() {
     const { data } = useSWR('/api/data', fetcher);
     return <div>Data: {data}</div>;
   }
   ```
   - If both `ComponentA` and `ComponentB` mount at the same time, only **one** request is sent instead of two.

### **Why Use Caching, Retries, and Deduping?**
✅ Improves performance by reducing redundant API calls  
✅ Enhances user experience by speeding up responses  
✅ Handles network failures more gracefully  
✅ Reduces server load  
