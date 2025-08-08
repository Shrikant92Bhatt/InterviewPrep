# React Interview Questions \& Coding Challenges (eBook Format)

## React Core Interview Questions

### 1. What is a Closure in React?

Describe closures, their importance in JavaScript, and how they're used with React, especially in event handlers and hooks.

#### Example:

```js
function makeCounter() {
  let count = 0;
  return function() {
    count++;
    return count;
  };
}
const counter = makeCounter();
console.log(counter()); // 1
console.log(counter()); // 2
```

### 2. Write a Higher-Order Component (HOC) Example

Explain HOCs as functions that take a component and return a new component.

#### Example:

```js
function withLogger(WrappedComponent) {
  return function(props) {
    console.log('Props:', props);
    return <WrappedComponent {...props} />;
  };
}
```

### 3. Closure Example with HOC

Illustrate how closures retain state inside an HOC.

#### Example:

```js
function withCount(WrappedComponent) {
  let count = 0; // closure variable
  return function(props) {
    count++;
    return <WrappedComponent count={count} {...props} />;
  };
}
```

### 4. Explain Reconciliation in React. What is React Fiber?

- **Reconciliation:** React's process to update the DOM efficiently by comparing the new virtual DOM with the previous one.
- **React Fiber:** React's underlying engine for scheduling, prioritization, and concurrency.

### 5. React Hooks

#### Core Hooks and Examples:

- **useState**

```js
const [count, setCount] = useState(0);
```

- **useEffect**

```js
useEffect(() => { document.title = count; }, [count]);
```

- **useContext**

```js
const value = useContext(MyContext);
```

- **useRef**

```js
const inputRef = useRef();
```

- **useMemo**

```js
const expensiveValue = useMemo(() => computeExpensive(a, b), [a, b]);
```

- **useCallback**

```js
const memoizedCallback = useCallback(() => { doSomething(a, b); }, [a, b]);
```

### 6. Design Patterns in React

#### a. Custom Hook

```js
function useCounter(initialValue = 0) {
  const [count, setCount] = useState(initialValue);
  const increment = () => setCount(c => c + 1);
  return [count, increment];
}
```

#### b. Render Props

```js
function DataProvider({ render }) {
  // fetch logic
  return render(data);
}
```

## Performance Optimization Concepts

### 7. Performance Improvement in React

- **Lazy Loading:**

```js
const LazyComp = React.lazy(() => import('./LazyComp'));
```

- **Memoization:**

```js
const memoizedValue = useMemo(() => compute(), [input]);
```

- **Debounce**
- **Throttling**

### 8. Concurrent Rendering

- **Suspense**

```js
<Suspense fallback={<div>Loading...</div>}>
  <LazyComponent />
</Suspense>
```

- **useTransition**

```js
const [isPending, startTransition] = useTransition();
startTransition(() => setValue(newValue));
```

- **useDeferredValue**

```js
const deferredValue = useDeferredValue(value);
```

### 9. Build a Custom Hook for useDebounce and useThrottle

#### useDebounce Example:

```js
function useDebounce(value, delay) {
  const [debounced, setDebounced] = useState(value);
  useEffect(() => {
    const handler = setTimeout(() => setDebounced(value), delay);
    return () => clearTimeout(handler);
  }, [value, delay]);
  return debounced;
}
```

#### useThrottle Example:

```js
function useThrottle(value, delay) {
  const [throttled, setThrottled] = useState(value);
  const lastRan = useRef(Date.now());
  useEffect(() => {
    if (Date.now() - lastRan.current >= delay) {
      setThrottled(value);
      lastRan.current = Date.now();
    }
  }, [value, delay]);
  return throttled;
}
```

## State Management \& React Internals

### 10. Redux and its Architecture

- **Redux:** Predictable state container for JS apps.
- **Architecture:** Store, Actions, Reducers, Middleware.

### 11. Redux vs Context API

|             | Redux                      | Context API                |
| :---------- | :------------------------- | :------------------------- |
| Use Case    | Large scale, complex state | Shared, simple state       |
| Boilerplate | More                       | Less                       |
| Middleware  | Supported                  | Not built-in               |
| Performance | Fine-tuned                 | Can cause extra re-renders |

### 12. useEffect vs useLayoutEffect

- **useEffect:** Runs _after_ paint. For async, side effects.
- **useLayoutEffect:** Runs _before_ paint. For DOM reads/writes.

### 13. BrowserRouter vs HashRouter

|                | BrowserRouter | HashRouter |
| :------------- | :------------ | :--------- |
| URL Format     | `/path`       | `#/path`   |
| Server Support | Needs config  | No config  |
| SEO Friendly   | Yes           | No         |

## Coding Challenge Section

### 1. Build CRUD Operation with Dummy API

- Use [jsonplaceholder.typicode.com](https://jsonplaceholder.typicode.com/) for fake REST.

```js
// Example with fetch & useEffect to load, add, edit, and delete posts
```

### 2. Build Timer Stopwatch (Reset / Pause / Start)

```js
// Use useState, useRef, useEffect: buttons for start, pause, reset
```

### 3. Prototype useEffect in Vanilla JS

```js
// Create a function that observes dependencies, calls callback when they change. Mimic useEffect behavior.
```

### 4. React setState "Batching" Example

**Given Code**:

```js
function increment() {
  setCounter(counter + 1);
  setCounter(counter + 1);
}
```

**Question:** Why does it increment by only 1?

- **Answer:** React batches updates. Both calls read the same value.

**Fix:**

```js
setCounter(prev => prev + 1);
setCounter(prev => prev + 1);
// Increments by 2
```

## More Advanced React \& JavaScript Questions

- What are controlled vs uncontrolled components?
- How do you optimize a React app for production?
- Explain error boundaries in React.
- What is React Profiler?
- Explain portals in React.
- How to handle memory leaks in React?
- What are React fragments?
- How does useImperativeHandle work?
- What is the difference between null, undefined, and NaN in JS?
- Difference between map, forEach, filter in JS.
- How do you protect routes in React?
- How does server-side rendering (SSR) differ from client-side rendering (CSR)?
- Explain suspense for data fetching.

## Example for Each Common React Hook

### useState

```js
const [count, setCount] = useState(0);
```

### useEffect

```js
useEffect(() => { console.log('mount'); }, []);
```

### useContext

```js
const value = useContext(MyContext);
```

### useReducer

```js
const [state, dispatch] = useReducer(reducer, initialState);
```

### useRef

```js
const inputRef = useRef();
```

### useCallback

```js
const memoized = useCallback(() => doSomething(a, b), [a, b]);
```

### useMemo

```js
const memoizedValue = useMemo(() => compute(a, b), [a, b]);
```

### useImperativeHandle

```js
useImperativeHandle(ref, () => ({ focus: () => { ... } }));
```

### useLayoutEffect

```js
useLayoutEffect(() => { /* runs synchronously after render, before paint */ }, []);
```

- **A simple Timer/Stopwatch code**
- **CRUD operations example for a Todo app using a dummy API**
- **Full, improved list for a Word document copy-paste**

# React Interview \& Coding eBook

(Organize with headings in Word)

## React Interview Questions (with Concepts \& Examples)

1. **Closure in React**
   _What is it? Show example usage in React components or hooks._
2. **Write a Higher Order Component (HOC)**
   _With coding example._
3. **Closure Example with HOC**
4. **Explain Reconciliation \& React Fiber**
5. **React Hooks:**
   - useState — _example included_
   - useEffect — _example included_
   - useContext
   - useRef
   - useCallback
   - useMemo
   - useReducer
   - useLayoutEffect
   - useImperativeHandle
6. **Design Patterns:**
   - Custom hook (with code sample)
   - Render Props (with code sample)
7. **Performance Optimization:**
   - Lazy Loading
   - Memoization
   - Debounce
   - Throttling
8. **Concurrent Rendering in React:**
   - Suspense
   - useTransition
   - useDeferredValue
9. **Build a Custom Hook:**
   - useDebounce (sample code)
   - useThrottle (sample code)
10. **Redux:**
    - Redux overview
    - Redux Architecture
11. **Redux vs Context API**
    _Comparison table_
12. **useEffect vs useLayoutEffect**
    _When to use which? Code sample._
13. **BrowserRouter vs HashRouter**
    _Comparison table_
14. **Other Advanced React/JS Questions**
    - Controlled vs uncontrolled components
    - React error boundaries
    - Portals
    - Fragments
    - SSR vs CSR
    - Route protection
    - Profiler
    - More (as in previous answer)

## Coding Challenges \& Examples

### 1. **Timer / Stopwatch Component (with Start, Pause, Reset)**

```jsx
import React, { useState, useRef } from 'react';

function Timer() {
  const [time, setTime] = useState(0);
  const [running, setRunning] = useState(false);
  const timerRef = useRef(null);

  const start = () => {
    if (!running) {
      setRunning(true);
      timerRef.current = setInterval(() => {
        setTime(prev => prev + 1);
      }, 1000);
    }
  };

  const pause = () => {
    setRunning(false);
    clearInterval(timerRef.current);
  };

  const reset = () => {
    setTime(0);
    setRunning(false);
    clearInterval(timerRef.current);
  };

  return (
    <div>
      <h1>Timer: {time} sec</h1>
      <button onClick={start} disabled={running}>Start</button>
      <button onClick={pause} disabled={!running}>Pause</button>
      <button onClick={reset}>Reset</button>
    </div>
  );
}
```

### 2. **CRUD Operations for a Todo App (using Dummy API)**

This sample uses the dummy API [jsonplaceholder.typicode.com]
**Assumptions:** For a real app, you’d handle errors, loading, and data normalization.

```jsx
import React, { useState, useEffect } from "react";

const API_URL = "https://jsonplaceholder.typicode.com/todos";

function TodoApp() {
  const [todos, setTodos] = useState([]);
  const [input, setInput] = useState("");

  // Fetch Todos
  useEffect(() => {
    fetch(`${API_URL}?_limit=5`)
      .then((res) => res.json())
      .then((data) => setTodos(data));
  }, []);

  // Add Todo
  const addTodo = () => {
    if (!input.trim()) return;
    fetch(API_URL, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ title: input, completed: false })
    })
      .then(res => res.json())
      .then(newTodo => setTodos([newTodo, ...todos]));
    setInput("");
  };

  // Toggle Completed
  const toggleTodo = (id) => {
    setTodos(todos.map(todo =>
      todo.id === id ? { ...todo, completed: !todo.completed } : todo
    ));
  };

  // Delete Todo
  const deleteTodo = (id) => {
    fetch(`${API_URL}/${id}`, { method: "DELETE" })
      .then(() => setTodos(todos.filter(todo => todo.id !== id)));
  };

  return (
    <div>
      <h1>Todo App</h1>
      <input value={input} onChange={e => setInput(e.target.value)} />
      <button onClick={addTodo}>Add Todo</button>
      <ul>
        {todos.map(todo => (
          <li key={todo.id} style={{
            textDecoration: todo.completed ? "line-through" : "none"
          }}>
            <input
              type="checkbox"
              checked={todo.completed}
              onChange={() => toggleTodo(todo.id)}
            />
            {todo.title}
            <button onClick={() => deleteTodo(todo.id)}>Delete</button>
          </li>
        ))}
      </ul>
    </div>
  );
}
```

### 3. **React setState Batching Example**

```jsx
function Counter() {
  const [counter, setCounter] = useState(0);

  function increment() {
    setCounter(counter + 1);
    setCounter(counter + 1); // increments by 1
  }

  // Solution (increments by 2):
  // setCounter(prev => prev + 1);
  // setCounter(prev => prev + 1);

  return (
    <>
      <div>{counter}</div>
      <button onClick={increment}>Increment</button>
    </>
  );
}
```



