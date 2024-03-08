# React.js

### Q : What is React?
A : React is a front-end and open-source JavaScript library which is useful in developing user interfaces specifically for applications with a single page. It is helpful in building complex and reusable user interface(UI) components of mobile and web applications as it follows the component-based approach.

* react simplify the creating of SPA by using reusable components.

* It supports server-side rendering.
* It will make use of the virtual DOM rather than real DOM (Data Object Model) as RealDOM manipulations are expensive.
* It follows unidirectional data binding or data flow.
* It uses reusable or composable UI components for developing the view.

* index.html is ebtry point of react app

### Q : Features of react.
A : 
* Uses JSX syntax, a syntax extension of JS that allows developers to write HTML in their JS code.
* It uses Virtual DOM instead of Real DOM considering that Real DOM manipulations are expensive.
* Supports server-side rendering which is useful for Search Engine Optimizations(SEO).
* Follows Unidirectional or one-way data flow or data binding.
* Uses reusable/composable UI components to develop the view.

### Q : What are the advantages of using React?
A : 
* Increases the application's performance with Virtual DOM.
* JSX makes code easy to read and write.
* It renders both on client and server side (SSR).
* Easy to integrate with frameworks (Angular, Backbone) since it is only a view library.
* Easy to write unit and integration tests with tools such as Jest.

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
### Q : What is Component?
A : In react, a component is reusable building block for creating UI.

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
A : State of a component is an object that holds some information that may change over the lifetime of the component. We should always try to make our state as simple as possible and minimize the number of stateful components.

State is similar to props, but it is private and fully controlled by the component ,i.e., it is not accessible to any other component till the owner component decides to pass it.

Let's create a user component with message state,
```
class User extends React.Component {
  constructor(props) {
    super(props)

    this.state = {
      message: 'Welcome to React world'
    }
  }

  render() {
    return (
      <div>
        <h1>{this.state.message}</h1>
      </div>
    )
  }
}
```

### Q : What are props in React?
A : Props are inputs to components. They are single values or objects containing a set of values that are passed to components on creation using a naming convention similar to HTML-tag attributes. They are data passed down from a parent component to a child component.

The primary purpose of props in React is to provide following component functionality:

* Pass custom data to your component.
* Trigger state changes.
* Use via this.props.reactProp inside component's render() method.

### Q : What is the difference between state and props?
A : Both props and state are plain JavaScript objects. While both of them hold information that influences the output of render, they are different in their functionality with respect to component. Props get passed to the component similar to function parameters whereas state is managed within the component similar to variables declared within a function.

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

### Q : What is "key" prop and what is the benefit of using it in arrays of elements?
A : A key is a special string attribute you should include when creating arrays of elements. Key prop helps React identify which items have changed, are added, or are removed.

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
componentWillMount
componentDidMount
componentWillReceiveProps
shouldComponentUpdate
componentWillUpdate
componentDidUpdate
componentWillUnmount

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

### Q : What is context?
Context provides a way to pass data through the component tree without having to pass props down manually at every level.

For example, authenticated users, locale preferences, UI themes need to be accessed in the application by many components.
```
const {Provider, Consumer} = React.createContext(defaultValue)
```

### Q : What is reconciliation?
A : When a component's props or state change, React decides whether an actual DOM update is necessary by comparing the newly returned element with the previously rendered one. When they are not equal, React will update the DOM. This process is called reconciliation.

### Q : What are the rules that must be followed while using React Hooks?
A :
* React Hooks must be called only at the top level. It is not allowed to call them inside the nested functions, loops, or conditions.
* It is allowed to call the Hooks only from the React Function Components.

### Q : Name a few techniques to optimize React app performance.
A : 
* Using useMemo( ) -
It is a React hook that is used for caching CPU-Expensive functions.
Sometimes in a React app, a CPU-Expensive function gets called repeatedly due to re-renders of a component, which can lead to slow rendering.
useMemo( ) hook can be used to cache such functions. By using useMemo( ), the CPU-Expensive function gets called only when it is needed.

* Using React.PureComponent -
It is a base component class that checks the state and props of a component to know whether the component should be updated.
Instead of using the simple React.Component, we can use React.PureComponent to reduce the re-renders of a component unnecessarily.
React.PureComponent is exactly the same as React.Component except that it handles the shouldComponentUpdate() method for you. When props or state changes, PureComponent will do a shallow comparison on both props and state. Component on the other hand won't compare current props and state to next out of the box. Thus, the component will re-render by default whenever shouldComponentUpdate is called.

* Maintaining State Colocation -
This is a process of moving the state as close to where you need it as possible.
Sometimes in React app, we have a lot of unnecessary states inside the parent component which makes the code less readable and harder to maintain. Not to forget, having many states inside a single component leads to unnecessary re-renders for the component.
It is better to shift states which are less valuable to the parent component, to a separate component.

* Lazy Loading -
 It is a technique used to reduce the load time of a React app. Lazy loading helps reduce the risk of web app performances to a minimum.

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

In this example, `<>` and `</>` are shorthand syntax for a fragment. It's equivalent to using `<React.Fragment>` and `</React.Fragment>`. The elements inside the fragment are siblings and can be rendered without introducing an additional div or other container element to the DOM.

Fragments help in keeping the HTML structure clean and avoiding unnecessary nesting, which can be beneficial for styling and layout purposes. They are especially handy when you need to return multiple elements from a component function without creating an artificial parent node in the rendered output.

### Q : Explain about types of Hooks in React.
A : 
* useState(): This functional component is used to set and retrieve the state.
* useEffect(): It enables for performing the side effects in the functional components.
* useContext(): It is used for creating common data that is to be accessed by the components hierarchy without having to pass the props down to each level.
* useRef() : It will permit creating a reference to the DOM element directly within the functional component.
* useLayoutEffect(): It is used for the reading layout from the DOM and re-rendering synchronously.
* useMemo() : This will be used for recomputing the memoized value when there is a change in one of the dependencies. This optimization will help for avoiding expensive calculations on each render.
* useCallback() : This is useful while passing callbacks into the optimized child components and depends on the equality of reference for the prevention of unneeded renders.

### Q : Diff between usememo and usecallback
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

### Q : What is What is context?
A : Context provides a way to pass data through the component tree without having to pass props down manually at every level.

For example, authenticated users, locale preferences, UI themes need to be accessed in the application by many components.
```
const { Provider, Consumer } = React.createContext(defaultValue);
```

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

### Q : How to optimize a react poject
A : 
Optimizing a React project involves improving its performance, reducing load times, and enhancing the user experience. Here are several techniques you can employ to optimize a React project:

1. **Code Splitting:**
   - Implement code splitting to split your bundle into smaller chunks. This allows you to load only the code that's needed for the current view, reducing initial load times. Use React.lazy() and Suspense for lazy loading components.

2. **Minification and Compression:**
   - Minify and compress your JavaScript, CSS, and HTML files to reduce file sizes. Tools like Webpack, UglifyJS, and Gzip compression can help optimize your assets for production.

3. **Image Optimization:**
   - Optimize images by compressing them without significantly impacting visual quality. Use tools like ImageMagick, Squoosh, or image compression plugins for Webpack to optimize images for the web.

4. **Bundle Analysis:**
   - Analyze your bundle size using tools like Webpack Bundle Analyzer to identify large dependencies or unnecessary code. Remove unused libraries or split large chunks to optimize bundle size.

5. **Server-Side Rendering (SSR):**
   - Implement server-side rendering to generate HTML on the server and improve initial page load times. Frameworks like Next.js provide built-in support for SSR, enabling better performance and SEO.

6. **Prefetching and Preloading:**
   - Prefetch or preload critical resources (e.g., JavaScript, CSS, images) for subsequent navigation using browser hints like `<link rel="prefetch">` or `<link rel="preload">`. This reduces latency and improves perceived performance.

7. **Caching:**
   - Implement browser caching to store static assets locally, reducing server requests for subsequent visits. Use Cache-Control headers or Service Workers to control caching behavior and improve performance.

8. **Tree Shaking:**
   - Enable tree shaking in your bundler (e.g., Webpack) to remove unused code and dependencies from your bundle. This helps reduce bundle size and improve load times.

9. **Memoization:**
   - Memoize expensive function calls or computations using libraries like memoize-one or useMemo() hook in React. Memoization prevents unnecessary recalculations and improves performance.

10. **Debouncing and Throttling:**
    - Use debouncing and throttling techniques to limit the frequency of expensive operations, such as resizing events or API requests. This prevents excessive resource consumption and improves responsiveness.

11. **Performance Monitoring:**
    - Monitor your application's performance using tools like Lighthouse, Google PageSpeed Insights, or New Relic. Identify and address performance bottlenecks to ensure optimal user experience.

12. **Error Handling and Logging:**
    - Implement error handling and logging mechanisms to capture and report errors in production. Use tools like Sentry or Rollbar to track and diagnose errors, ensuring a smooth user experience.

13. **Optimized Rendering:**
    - Optimize rendering performance by minimizing the number of re-renders and optimizing render methods. Use shouldComponentUpdate(), React.memo(), or PureComponent to prevent unnecessary renders.

14. **Lazy Loading and Code Splitting:**
    - Implement lazy loading and code splitting to load components and resources asynchronously as needed. This improves initial load times and reduces the time to interactive.

15. **Optimized Network Requests:**
    - Minimize network requests by combining and optimizing API calls. Use techniques like batch requests, caching, or GraphQL to reduce the number of round trips to the server.

By applying these optimization techniques, you can significantly improve the performance, user experience, and overall efficiency of your React project. Regularly monitor and analyze performance metrics to identify areas for improvement and ensure that your application remains optimized over time.

## React Router

### Q : What is React Router?
A : React Router is a powerful routing library built on top of React that helps you add new screens and flows to your application incredibly quickly, all while keeping the URL in sync with what's being displayed on the page.

### Q : What are the <Router> components of React Router v4?
A : React Router v4 provides below 3 <Router> components:

* <BrowserRouter>
* <HashRouter>
* <MemoryRouter>
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
