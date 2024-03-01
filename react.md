# React.js

### Q : What is React?
A : React is a front-end and open-source JavaScript library which is useful in developing user interfaces specifically for applications with a single page. It is helpful in building complex and reusable user interface(UI) components of mobile and web applications as it follows the component-based approach.

* It supports server-side rendering.
* It will make use of the virtual DOM rather than real DOM (Data Object Model) as RealDOM manipulations are expensive.
* It follows unidirectional data binding or data flow.
* It uses reusable or composable UI components for developing the view.

### Q : What are the advantages of using React?
A : 
* Use of Virtual DOM to improve efficiency: React uses virtual DOM to render the view. As the name suggests, virtual DOM is a virtual representation of the real DOM. Each time the data changes in a react app, a new virtual DOM gets created. Creating a virtual DOM is much faster than rendering the UI inside the browser. Therefore, with the use of virtual DOM, the efficiency of the app improves.

* Gentle learning curve: React has a gentle learning curve when compared to frameworks like Angular. Anyone with little knowledge of javascript can start building web applications using React.

* SEO friendly: React allows developers to develop engaging user interfaces that can be easily navigated in various search engines. It also allows server-side rendering, which boosts the SEO of an app.

* Reusable components: React uses component-based architecture for developing applications. Components are independent and reusable bits of code. These components can be shared across various applications having similar functionality. The re-use of components increases the pace of development.

* Huge ecosystem of libraries to choose from: React provides you with the freedom to choose the tools, libraries, and architecture for developing an application based on your requirement.

### Q : What is JSX?
A : JSX stands for JavaScript XML. It allows us to write HTML inside JavaScript and place them in the DOM without using functions like appendChild( ) or createElement( ). As stated in the official docs of React, JSX provides syntactic sugar for React.createElement( ) function.

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

### Q : What are the differences between functional and class components?
A : There are mainly two type

Before the introduction of Hooks in React, functional components were called stateless components and were behind class components on a feature basis. After the introduction of Hooks, functional components are equivalent to class components.

Although functional components are the new trend, the react team insists on keeping class components in React. Therefore, it is important to know how these components differ.

* functional component

```
function card(props){
   return(
      <div className="main-container">
        <h2>Title of the card</h2>
      </div>
    )
   }
   const card = (props) =>{
    return(
      <div className="main-container">
        <h2>Title of the card</h2>
      </div>
    )
   }
```

* class based component
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

If the component needs state or lifecycle methods then use class component otherwise use function component. However, from React 16.8 with the addition of Hooks, you could use state , lifecycle methods and other features that were only available in class component right in your function component. *So, it is always recommended to use Function components, unless you need a React functionality whose Function component equivalent is not present yet, like Error Boundaries *


### Q : What is the virtual DOM? How does react use the virtual DOM to render the UI?
A : As stated by the react team, virtual DOM is a concept where a virtual representation of the real DOM is kept inside the memory and is synced with the real DOM by a library such as ReactDOM.


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

* Uncontrolled component: 
In an uncontrolled component, the value of the input element is handled by the DOM itself. Input elements inside uncontrolled components work just like normal HTML input form elements.
The state of the input element is handled by the DOM. Whenever the value of the input element is changed, event-based callbacks are not called. Basically, react does not perform any action when there are changes made to the input element.

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

