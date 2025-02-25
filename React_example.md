## List diplay and remove perticular item from list
```javascrip
import React, { useRef, useState } from 'react'
import Confetti from 'js-confetti'
import './style.css'

const confetti = new Confetti()

const App = () => {
  const [name, setName] = useState('')
  const [age, setAge] = useState(0)
  const [list, setList] = useState([])

  const onSubmit = () => {
    setList((prev) => [...prev, {name, age}])
    setName('')
    setAge(0)
  }

   const onDelete = (index) => {
      // const newList = [...list];
      // newList.splice(index, 1);
      // setList(newList)
     let newList = list.filter((obj, i) => i!==index);
     setList(newList)
  }

  return (
  <>
    {list.length > 0 &&  <ul>  
        {list.map((obj, index)=>(
          <li>
            {obj.name}
            {obj.age}
            <button onClick={(e)=>{onDelete(index)}}> Remove from List </button>
          </li>
        ))}
      </ul>}
  <div>
  <input
    value={name}
    type='text'
    onChange={(e)=>setName(e.target.value)}/>
    <input
    value={age}
    type='number'
    onChange={(e)=>setAge(e.target.value)}/>
    <button onClick={(e)=>{onSubmit()}}> Add In List </button>
  </div>
  </>
  )
}
export default App
```

## Simple List Display and Pagination

```javascript
import React, { useState } from 'react';

export function App(props) {
  const items = [
    'Apple', 'Banana', 'Cherry', 'Orange', 'Melon',
    'Keri', 'Jamun', 'Berry', 'Grapes',
  ];
  const perPage = 3;
  const [startIndex, SetStartIndex] = useState(0);

  let displayArray = items.slice(startIndex, startIndex + perPage);

  const nextList = () => {
    if (startIndex + perPage < items.length) {
      SetStartIndex(startIndex + perPage);
    } else {
      SetStartIndex(0);
    }
  };

  return (
    <div className='App'>
      <h1>Display list</h1>
      <ul>
        {displayArray.map((item, i) => (
          <li key={i}>{item}</li>
        ))}
      </ul>
      <button onClick={nextList}>Next</button>
    </div>
  );
}
```

## simple ToDO with react class component
```
import React, { Component } from "react";

class App extends Component {
  constructor(props) {
    super(props);
    this.state = { todos: [], task: "" };
  }

  onChangeTask = (e) => {
    this.setState({
      task: e.target.value
    });
  };

  addTask = () => {
    let { todos, task } = this.state;
    todos.push(task);
    this.setState(
      {
        todos: todos,
        task: ""
      },
      () => {
        console.log(this.state);
      }
    );
  };

  render() {
    return (
      <>
        <div className="App">
          <h1>Todo</h1>
          <input
            type="text"
            value={this.state.task}
            onChange={(e) => {
              this.onChangeTask(e);
            }}
          />
          <button onClick={this.addTask} disabled={!this.state.task}>
            Add
          </button>
        </div>
        <ul>
          {this.state.todos.length > 0 && this.state.todos.map((todo, index) => (
            <li key={index}>{todo}</li>
          ))}
        </ul>
      </>
    );
  }
}

export default App;
```

## todo with functional components
```
import React, { useState } from "react";
import { render } from "react-dom";

// Functional component
const TodoDisplay = (props) => {
  return <li>{props.todo}</li>;
};

// Main App component
// renders a list of Messages using data from messages.json
const App = () => {
  const [task, setTask] = useState("");
  const [todos, setTodos] = useState([]);
  const addTask = () => {
    todos.push(task);
    setTodos(todos);
    setTask("");
  };

  return (
    <>
      <h2>To Do</h2>
      <div>
        <input value={task} onChange={(e) => setTask(e.target.value)} />
        <button onClick={addTask} disabled={!task}>
          Add Task
        </button>
      </div>
      <ul>
        {todos.length > 0 &&
          todos.map((todo, i) => <TodoDisplay key={i} todo={todo} />)}
      </ul>
    </>
  );
};

render(<App />, document.getElementById("root"));
```
