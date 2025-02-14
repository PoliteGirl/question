# React.js

### Q : What is React?  
A : React is an open-source JavaScript library for building user interfaces, particularly for single-page applications (SPAs). It follows a **component-based approach**, allowing developers to create reusable UI components for web and mobile applications.  

* Simplifies SPA development by using reusable components.  
* Supports **server-side rendering (SSR)** for better SEO.  
* Uses **Virtual DOM** instead of Real DOM to improve performance.  
* Follows **unidirectional data flow**: Data flows from parent to child via props, ensuring better state management.  
* Encourages **reusable and composable UI components** for a modular development approach.  
* The **index.html** file serves as the entry point of a React app.  

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
A : 
* with help of babel library jsx code gets convert to js code that browser can understand. Babel is a transpiler.

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
### **1️⃣ API Requests Without Cleanup**
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
### **2️⃣ Event Listeners Not Removed**
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

### **3️⃣ Timers (`setInterval`, `setTimeout`) Not Cleared**
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

### **4️⃣ References to DOM Elements**
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

### **Common Memory Leaks & Fixes**  

✅ **Not Cleaning Event Listeners**  
```jsx
useEffect(() => {
  const handler = () => console.log("Resizing...");
  window.addEventListener("resize", handler);

  return () => window.removeEventListener("resize", handler); // ✅ Cleanup
}, []);
```

✅ **Unfinished API Calls**  
```jsx
useEffect(() => {
  const controller = new AbortController();
  fetch("/api/data", { signal: controller.signal }).then(res => res.json());

  return () => controller.abort(); // ✅ Cleanup
}, []);
```

✅ **Not Clearing Intervals**  
```jsx
useEffect(() => {
  const interval = setInterval(() => console.log("Running..."), 1000);

  return () => clearInterval(interval); // ✅ Cleanup
}, []);
```

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
* controlled : 
In a controlled component, the value of the input element is controlled by React. We store the state of the input element inside the code, and by using event-based callbacks, any changes made to the input element will be reflected in the code as well.
When a user enters data inside the input element of a controlled component, onChange function gets triggered and inside the code, we check whether the value entered is valid or invalid. If the value is valid, we change the state and re-render the input element with the new value.
```
handleChange(event) {
  this.setState({value: event.target.value.toUpperCase()})
}
```

* Uncontrolled component: 
In an uncontrolled component, the value of the input element is handled by the DOM itself. Input elements inside uncontrolled components work just like normal HTML input form elements.
The state of the input element is handled by the DOM. Whenever the value of the input element is changed, event-based callbacks are not called. Basically, react does not perform any action when there are changes made to the input element.
```
class UserProfile extends React.Component {
  constructor(props) {
    super(props);
    this.handleSubmit = this.handleSubmit.bind(this);
    this.input = React.createRef();
  }

  handleSubmit(event) {
    alert("A name was submitted: " + this.input.current.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          {"Name:"}
          <input type="text" ref={this.input} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```
Whenever use enters data inside the input field, the updated data is shown directly. To access the value of the input element, we can use ref.

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
HOC can be used for many use cases:

* Code reuse, logic and bootstrap abstraction.
* Render hijacking.
* State abstraction and manipulation.
* Props manipulation.

### Q : What is reconciliation?
A : When a component's props or state change, React decides whether an actual DOM update is necessary by comparing the newly returned element with the previously rendered one. When they are not equal, React will update the DOM. This process is called reconciliation.

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

### Q : Diff between usememo and usecallback
A : 
useMemo
useMemo is used to memoize a value (usually an object, function, or any complex computation) and to avoid recalculating it on every render unless the dependencies change.
It takes a function and an array of dependencies as arguments. The function is only re-executed when one of the dependencies has changed.
It is useful when you have a costly computation that doesn't need to be recalculated unless its dependencies change.
Example:
```
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```
useCallback
useCallback is used to memoize a callback function to prevent unnecessary renders of components that rely on that callback.
It takes a callback function and an array of dependencies, similar to useMemo. The difference is that useCallback returns a memoized version of the callback itself.
It is useful when you want to prevent the recreation of callback functions in child components, which could cause unnecessary re-renders.
Example:
```
const memoizedCallback = useCallback(() => {
  doSomethingWith(a, b);
}, [a, b]);
```
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

### **The Role of Cleanup in Your Case:**

In your case, you're using `axios` to fetch data from an API inside the `useEffect` hook. But there’s a potential issue when the component unmounts before the request completes:

1. **What could happen?**
   - If the component unmounts (for example, when you navigate away from the page) before the API request completes, the `setState` call in the `axios` `.then()` or `.catch()` could try to update the state of a component that is no longer in the DOM.
   - This would result in a **memory leak** and a warning like:
     ```
     Can't perform a React state update on an unmounted component.
     ```
  
2. **Why use `cleanup` here?**
   - To **prevent state updates** when the component unmounts, you can use the cleanup function to cancel or ignore updates. In this case, we use a flag (`isMounted`) to check if the component is still mounted before trying to update the state.
   - The cleanup function (inside `useEffect`) runs when:
     - The component unmounts.
     - The effect is about to run again (if the dependency array changes).

3. **How does the cleanup work here?**
   - The `isMounted` flag ensures that the `setData` and `setError` functions are only called if the component is still present in the DOM.
   - When the component unmounts, `isMounted` is set to `false` in the cleanup function, and if the API call completes after the component unmounts, we skip the state update because `isMounted` will be `false`.

### **Code Breakdown:**

```jsx
useEffect(() => {
  // Flag to track if component is mounted
  let isMounted = true; 
  
  // API request
  axios.get("/api/data")
    .then((response) => {
      // Only update state if the component is still mounted
      if (isMounted) {
        setData(response.data);
        setLoading(false);
      }
    })
    .catch((err) => {
      // Handle error, but only update state if component is still mounted
      if (isMounted) {
        setError(err.message);
        setLoading(false);
      }
    });

  // Cleanup function that runs when component unmounts
  return () => {
    isMounted = false;
  };
}, []); // Empty dependency array means this effect runs only once on mount
```

### **Why Is This Cleanup Necessary?**
1. **Prevent Memory Leaks:** If an asynchronous task like a network request is still running when the component unmounts, **React cannot update the state** of the unmounted component, and doing so can cause **memory leaks**.
2. **Improve Performance:** Cleanup ensures that you don’t perform unnecessary operations (like API calls or event listeners) once the component is no longer in the DOM.
3. **Avoid Warnings:** By preventing state updates on unmounted components, you avoid the React warning about updating an unmounted component.

### **Is Cleanup Always Necessary?**
No, cleanup is not always required, but it's a **best practice** when dealing with asynchronous tasks, subscriptions, or timers in `useEffect`.

- **Necessary**: If you're making an API request, setting up event listeners, or using `setTimeout`/`setInterval`.
- **Not Necessary**: If the effect doesn't cause side effects that need to be cleaned up, such as simple state changes or effects that don't interact with outside resources.

### **Summary of Cleanup:**
- **Cleanup function** inside `useEffect` helps ensure that no **state updates or side effects** occur after a component unmounts.
- In this case, it prevents trying to **set state** when the component is no longer in the DOM.
- It’s important for asynchronous operations (like API calls) to ensure **no errors or memory leaks** occur.

### **Example: Cleanup an Event Listener**
```jsx
import React, { useState, useEffect } from "react";

const MouseTracker = () => {
  const [position, setPosition] = useState({ x: 0, y: 0 });

  const updateMousePosition = (e) => {
    setPosition({ x: e.clientX, y: e.clientY });
  };

  useEffect(() => {
    // Adding event listener when component mounts
    window.addEventListener("mousemove", updateMousePosition);

    // Cleanup function to remove event listener
    return () => {
      window.removeEventListener("mousemove", updateMousePosition);
      console.log("Cleanup: Event listener removed");
    };
  }, []); // Runs only once when component mounts

  return (
    <div>
      <h1>Mouse Position</h1>
      <p>X: {position.x}, Y: {position.y}</p>
    </div>
  );
};

export default MouseTracker;
```

### **How Cleanup Works Here**
- **When the component mounts**, the `mousemove` event listener is attached.
- **When the component unmounts**, the event listener is removed inside the `return` function of `useEffect`.
- This ensures **no memory leaks** and prevents unnecessary event listeners from staying active.

### **Other Common Use Cases for Cleanup**
1. **Clearing Timers:**
   ```jsx
   useEffect(() => {
     const timer = setInterval(() => console.log("Running..."), 1000);
     return () => clearInterval(timer);
   }, []);
   ```
2. **Aborting API Requests:**
   ```jsx
   useEffect(() => {
     const controller = new AbortController();
     fetch("https://api.example.com/data", { signal: controller.signal });

     return () => controller.abort(); // Cleanup API call
   }, []);
   ```

```
import React, { useEffect } from "react";

    const Timer = () => {
      const interval = React.useRef();
      const startGame = () => {
        interval.current = setInterval(() => {
          //code
        }, 3000);
      };
      React.useEffect(() => {
        return () => {
          clearInterval(interval.current);
        };
      }, []);
    };
    
    export default Timer;
```
### Q : Why is useEffect often bad practice
A :
**Why is `useEffect` Often Considered Bad Practice?**  

While `useEffect` is useful for side effects, **misusing it can lead to issues** like unnecessary re-renders, performance problems, and complex logic.  

**Common Issues with `useEffect`**  

1️⃣ **Unnecessary Effects** → Using `useEffect` for logic that can be done directly in the component.  
   - **Example:** Setting state based on props inside `useEffect` instead of directly computing it.  

2️⃣ **Dependency Issues** → Wrong dependencies can cause infinite loops or stale data.  
   - **Fix:** Always include dependencies carefully to avoid unnecessary re-executions.  

3️⃣ **Performance Bottlenecks** → Running expensive computations inside `useEffect`.  
   - **Fix:** Use **memoization (`useMemo`, `useCallback`)** when needed.  

4️⃣ **Tightly Coupled Code** → Business logic gets mixed with side effects.  
   - **Fix:** Extract reusable logic into **custom hooks**.  

5️⃣ **Memory Leaks** → Not cleaning up subscriptions, event listeners, or timers.  
   - **Fix:** Always return a **cleanup function** inside `useEffect`.  

### **When to Avoid `useEffect`?**  
❌ **Computing derived state** → Use `useState` or direct calculations instead.  
❌ **Synchronizing props/state unnecessarily** → Instead, compute values inside render.  
❌ **Fetching data on every render** → Use caching or memoization instead.  

### **When to Use `useEffect`?**  
✅ **Fetching data** (with proper dependencies).  
✅ **Subscribing to events, timers, or listeners** (with cleanup).  
✅ **Interacting with the DOM** (like animations or manual scroll handling).  

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

### Q : HOw to do Caching in react api call
Caching API responses helps improve performance by avoiding unnecessary network requests. Here are a few ways to implement caching in React:

### **1️⃣ Using `React Query` (Recommended)**
🔹 **React Query** automatically caches and updates API calls efficiently.
```jsx
import { useQuery } from "react-query";
import axios from "axios";

const fetchData = async () => {
  const { data } = await axios.get("https://api.example.com/data");
  return data;
};

function MyComponent() {
  const { data, error, isLoading } = useQuery("myData", fetchData, {
    staleTime: 5 * 60 * 1000, // Cache for 5 minutes
  });

  if (isLoading) return <p>Loading...</p>;
  if (error) return <p>Error!</p>;

  return <div>{JSON.stringify(data)}</div>;
}
```
✅ **Benefits:**  
- Automatic caching and revalidation  
- Background updates  
- Reduces unnecessary API calls  

---

### **2️⃣ Using `useRef` for Simple Caching**
🔹 Store API response in a `useRef` to persist data across renders.
```jsx
import { useState, useEffect, useRef } from "react";
import axios from "axios";

function MyComponent() {
  const [data, setData] = useState(null);
  const cache = useRef({}); // Store cached responses

  useEffect(() => {
    const fetchData = async () => {
      const url = "https://api.example.com/data";
      if (cache.current[url]) {
        setData(cache.current[url]); // Use cached data
      } else {
        const response = await axios.get(url);
        cache.current[url] = response.data; // Cache the response
        setData(response.data);
      }
    };
    fetchData();
  }, []);

  return <div>{JSON.stringify(data)}</div>;
}
```
✅ **Use case:**  
- Simple caching without external libraries  
- Stores data only for the session  

### **3️⃣ Using LocalStorage for Persistent Caching**
🔹 Store API responses in **localStorage** to persist even after a page reload.
```jsx
import { useState, useEffect } from "react";
import axios from "axios";

function MyComponent() {
  const [data, setData] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      const cachedData = localStorage.getItem("myData");
      if (cachedData) {
        setData(JSON.parse(cachedData));
      } else {
        const response = await axios.get("https://api.example.com/data");
        localStorage.setItem("myData", JSON.stringify(response.data));
        setData(response.data);
      }
    };
    fetchData();
  }, []);

  return <div>{JSON.stringify(data)}</div>;
}
```
✅ **Use case:**  
- Data persists even after a page reload  
- Good for rarely changing API data  

### **Which One to Use?**
| Method | When to Use? | Pros | Cons |
|--------|-------------|------|------|
| **React Query** | Best for API-heavy apps | Auto caching & background updates | Requires dependency |
| **useRef** | Simple caching within a session | No storage overhead | Data resets on refresh |
| **localStorage** | Persistent caching across sessions | No extra library needed | Storage limits |

📌 **Recommendation:**  
Use **React Query** for scalable solutions & **localStorage** for persistent data.

### Q : How to do read and writes with a caching library like apollo or react-query
A : 
### **Reading and Writing with Apollo & React Query (Caching Library)**  

Both **Apollo Client** and **React Query** provide caching mechanisms for efficient data fetching and updates. Here's how you can **read and write data** using both libraries.

---

## **1️⃣ Using Apollo Client (GraphQL Caching)**  

### **🔹 Read Data (Query with Cache)**
Apollo caches responses by default, and it automatically updates components when data changes.  

```jsx
import { gql, useQuery } from "@apollo/client";

const GET_USER = gql`
  query GetUser($id: ID!) {
    user(id: $id) {
      id
      name
      email
    }
  }
`;

function UserProfile({ userId }) {
  const { data, loading, error } = useQuery(GET_USER, {
    variables: { id: userId },
    fetchPolicy: "cache-first", // Uses cache if available
  });

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error...</p>;

  return <div>{data.user.name}</div>;
}
```
✅ **`fetchPolicy` Options:**  
- `cache-first` → Default (uses cache if available)  
- `network-only` → Always fetch from server  
- `cache-only` → Use only cached data  
- `cache-and-network` → Show cached data, then update from API  

---

### **🔹 Write Data (Mutation + Cache Update)**
After a mutation, update the cache to reflect changes in UI.

```jsx
import { gql, useMutation } from "@apollo/client";

const UPDATE_USER = gql`
  mutation UpdateUser($id: ID!, $name: String!) {
    updateUser(id: $id, name: $name) {
      id
      name
    }
  }
`;

function UpdateUserName({ userId }) {
  const [updateUser] = useMutation(UPDATE_USER, {
    update(cache, { data: { updateUser } }) {
      cache.modify({
        id: cache.identify(updateUser), // Identify cache entry
        fields: {
          name() {
            return updateUser.name; // Update name field
          },
        },
      });
    },
  });

  return (
    <button onClick={() => updateUser({ variables: { id: userId, name: "New Name" } })}>
      Update Name
    </button>
  );
}
```
✅ **Why Use `cache.modify`?**  
- Ensures UI updates without extra refetching  
- Keeps Apollo’s cache in sync  

---

## **2️⃣ Using React Query (REST API Caching)**  

### **🔹 Read Data (Query with Cache)**
React Query automatically caches data and keeps it fresh.

```jsx
import { useQuery } from "react-query";
import axios from "axios";

const fetchUser = async ({ queryKey }) => {
  const [, id] = queryKey;
  const { data } = await axios.get(`https://api.example.com/users/${id}`);
  return data;
};

function UserProfile({ userId }) {
  const { data, isLoading, error } = useQuery(["user", userId], fetchUser, {
    staleTime: 1000 * 60 * 5, // Cache for 5 minutes
  });

  if (isLoading) return <p>Loading...</p>;
  if (error) return <p>Error...</p>;

  return <div>{data.name}</div>;
}
```
✅ **Cache Strategies in React Query:**  
- `staleTime` → Time before data is considered "stale"  
- `cacheTime` → Time before unused data is removed  

---

### **🔹 Write Data (Mutation + Cache Update)**
React Query's `useMutation` handles API updates and cache invalidation.

```jsx
import { useMutation, useQueryClient } from "react-query";
import axios from "axios";

const updateUser = async ({ id, name }) => {
  return axios.put(`https://api.example.com/users/${id}`, { name });
};

function UpdateUserName({ userId }) {
  const queryClient = useQueryClient();
  const mutation = useMutation(updateUser, {
    onSuccess: () => {
      queryClient.invalidateQueries(["user", userId]); // Refetch user data
    },
  });

  return (
    <button onClick={() => mutation.mutate({ id: userId, name: "New Name" })}>
      Update Name
    </button>
  );
}
```
✅ **Why Use `invalidateQueries`?**  
- Ensures UI fetches fresh data  
- Automatically refetches data after a mutation  

---

## **📌 Which One to Use?**
| Feature | Apollo Client (GraphQL) | React Query (REST) |
|---------|----------------|----------------|
| Best For | GraphQL APIs | REST APIs |
| Cache Type | Normalized Cache | Query-based Cache |
| Auto Cache Update | Yes (with `cache.modify`) | Yes (with `invalidateQueries`) |
| Fetch Policy | `cache-first`, `network-only`, etc. | `staleTime`, `cacheTime` |

🚀 **Choose Apollo for GraphQL** and **React Query for REST APIs**!

### Q : What is wrong with using async/await in a useEffect hook in reference to the below code snippet?

function TestComponent() {
  const [data, setData] = useState([]);
 useEffect(() => {
	const fetchData = async () => {
  	const response = await fetch("/api/data");
  	const json = await response.json();
  	setData(json);
	};
	fetchData();
  }, []);
   return <div>{data.map((d) => <p>{d.text}</p>)}</div>;
}
A : ### **Issue with Using `async/await` in `useEffect`**  

The issue in the given code is that `useEffect` **cannot** directly handle an `async` function because it expects the return value to be either **`undefined` or a cleanup function**, but an `async` function always returns a **Promise**.

---

### **Why is this a Problem?**
- `useEffect(() => { async function() {} })` **returns a Promise**, which React **does not handle** properly.
- **React might show a warning**, and unexpected behavior can occur.

---

### **How to Fix It?**
✅ **Solution: Use an Inside Async Function**  
```jsx
useEffect(() => {
  const fetchData = async () => {
    try {
      const response = await fetch("/api/data");
      const json = await response.json();
      setData(json);
    } catch (error) {
      console.error("Error fetching data:", error);
    }
  };

  fetchData();
}, []);
```
**Why this works?**  
- The async function is **declared inside `useEffect`**, but `useEffect` itself remains **synchronous**.  

---

### **Alternative: Use an Immediately Invoked Function Expression (IIFE)**
```jsx
useEffect(() => {
  (async () => {
    const response = await fetch("/api/data");
    const json = await response.json();
    setData(json);
  })();
}, []);
```
This avoids defining a separate function inside `useEffect`.

---

### **Best Practice: Use `AbortController` to Prevent Memory Leaks**
To **prevent setting state after unmounting**, use **`AbortController`**:
```jsx
useEffect(() => {
  const controller = new AbortController();
  const fetchData = async () => {
    try {
      const response = await fetch("/api/data", { signal: controller.signal });
      const json = await response.json();
      setData(json);
    } catch (error) {
      if (error.name !== "AbortError") {
        console.error("Fetch error:", error);
      }
    }
  };

  fetchData();

  return () => controller.abort(); // Cleanup on unmount
}, []);
```

---

### **Summary**
❌ **Avoid** `useEffect(async () => {...})` because it returns a Promise.  
✅ **Wrap `async` function inside `useEffect`** and call it explicitly.  
✅ **Use `AbortController` to prevent memory leaks** in API calls.  

### Q : What will be the behaviour of the useRef and useCallback hooks in the below code snippet?

import React, { useState, useRef, useCallback } from "react";
 function App() {
  const [count, setCount] = useState(0);
  const countRef = useRef(count);
 
  const increment = useCallback(() => {
	countRef.current = countRef.current + 1;
	setCount(countRef.current);
  }, []);
 
  return (
	<div>
  	<button onClick={increment}>Increment</button>
  	<p>Count: {count}</p>
	</div>
  );
}
 export default App;
A : ### **Behavior of `useRef` and `useCallback` in the Given Code**  

#### **1️⃣ Behavior of `useRef(count)`**
- `useRef` **does not trigger re-renders** when its `.current` value changes.  
- Initially, `countRef.current` is set to `count` (which is `0`).  
- However, it **does not automatically update when `count` changes** because `useRef` does not cause re-renders like `useState`.

#### **2️⃣ Behavior of `useCallback`**
- The `increment` function is **memoized** using `useCallback`, meaning it will not be re-created unless its dependencies change.  
- But since the dependency array is **empty (`[]`)**, `increment` is **created only once** when the component mounts.  

---

### **What Happens When You Click the Button?**
1. `countRef.current = countRef.current + 1;`  
   - This updates the **ref value** (`countRef.current`) manually, but it **does not re-render the component**.  

2. `setCount(countRef.current);`  
   - This updates `count`, triggering a re-render.  

3. **However, there's a problem!**  
   - Since `useCallback` has an **empty dependency array**, `increment` **always captures the initial `countRef.current = 0`**.  
   - Even though `countRef.current` updates internally, **the function doesn't update with the latest state**.  

---

### **Issue: Stale Closure Problem**
The function does not get the latest `countRef.current` because `increment` was **created only once** and never re-created.  

#### **How to Fix It?**
✅ **Add `countRef.current` as a Dependency in `useCallback`**
```jsx
const increment = useCallback(() => {
  countRef.current = countRef.current + 1;
  setCount(countRef.current);
}, [countRef.current]); // ✅ Ensures `useCallback` updates correctly
```

✅ **Or Use `setCount(prev => prev + 1)` Directly**
```jsx
const increment = useCallback(() => {
  setCount(prev => prev + 1);
}, []);
```
This removes the need for `useRef` entirely.

---

### **Summary**
🔹 **`useRef` does not trigger re-renders**, so updating `countRef.current` alone won't reflect changes.  
🔹 **`useCallback` with `[]` captures stale values**, leading to unexpected behavior.  
🔹 **Fix by adding dependencies or using functional `setCount(prev => prev + 1)`**.  

### Q : What will be the behaviour of the useRef and useCallback hooks in the below code snippet?

import React, { useState, useRef, useCallback } from "react";
 function App() {
  const [count, setCount] = useState(0);
  const countRef = useRef(count);
 
  const increment = useCallback(() => {
	countRef.current = countRef.current + 1;
	setCount(countRef.current);
  }, []);
 
  return (
	<div>
  	<button onClick={increment}>Increment</button>
  	<p>Count: {count}</p>
	</div>
  );
}
 export default App;
---
A : ### **Behavior of `useRef` & `useCallback` in Given Code**  

1. **`useRef` does not trigger re-renders**, so updating `countRef.current` alone won't update the UI.  
2. **`useCallback([])` captures stale values**, meaning `increment` always uses the **initial** `countRef.current = 0`.  
3. **Fix:** Use a dependency or functional update:  
   ```jsx
   const increment = useCallback(() => {
     setCount(prev => prev + 1);
   }, []);
   ```
✅ **This removes the need for `useRef` and ensures correct updates.**

### Q : How can you optimize the handling of async data promises in the below code?

import { useCallback, useEffect } from "react";
 function TestComponent(props) {
  const fetchData = useCallback(async () => {
	const response = await fetch(/api/data/${props.id});
	const json = await response.json();
	return json;
  }, [props.id]);
 
  useEffect(() => {
    const dataPromise = fetchData();
	// Do something with the data promise
	return () => {
  	// Cancel the data promise
	};
  }, [fetchData]);
   return <div>My Component</div>;
}

A :  ### **Optimizing Async Data Handling in `useEffect`**  

#### **Issues in the Current Code:**
1. **Uncontrolled Promise Handling:**  
   - `fetchData()` returns a promise, but its resolution is not handled properly.  

2. **Potential Memory Leak:**  
   - If `props.id` changes or the component unmounts, the previous request **may still resolve**, updating stale state.  

3. **No Cancellation of Fetch Requests:**  
   - There's no way to abort the previous request when `props.id` changes.  

---

### **Optimized Approach**
✅ **Handle async logic inside `useEffect` properly**  
✅ **Use `AbortController` to cancel outdated fetch requests**  
✅ **Update state only when the component is still mounted**  

### **Optimized Code:**
```jsx
import { useCallback, useEffect, useState } from "react";

function TestComponent({ id }) {
  const [data, setData] = useState(null);

  const fetchData = useCallback(async (signal) => {
    try {
      const response = await fetch(`/api/data/${id}`, { signal });
      if (!response.ok) throw new Error("Fetch failed");
      const json = await response.json();
      setData(json);
    } catch (error) {
      if (error.name !== "AbortError") {
        console.error("Fetch error:", error);
      }
    }
  }, [id]);

  useEffect(() => {
    const controller = new AbortController();
    fetchData(controller.signal);

    return () => controller.abort(); // Cancel fetch on unmount or id change
  }, [fetchData]);

  return <div>{data ? JSON.stringify(data) : "Loading..."}</div>;
}

export default TestComponent;
```

---

### **Key Optimizations:**
✅ **Uses `AbortController` to prevent stale requests**  
✅ **Handles errors gracefully**  
✅ **Only updates state when the component is still active**  

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
