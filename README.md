# React-Interview-Questions

### Table of Contents

1. [What is difference between useMemo and useCallback?](#what-is-difference-between-usememo-and-usecallback-)
2. [Explain Life Cycle Methods in class based components?](#explain-life-cycle-methods-in-class-based-components-)
3. [What Hooks have you used?](#what-hooks-have-you-used?-)
4. [What is the purpose of useCallback?](#what-is-the-purpose-of-usecallback-)
5. [What are Class-based Lifecycle methods?](#q-what-are-class-based-lifecycle-methods-)
6. [How can you achieve componentDidMount, componentDidUpdate & componentDidUnMount in a functional-based component?](#how-can-you-achieve-componentdidmount-componentdidupdate--componentdidunmount-in-a-functional-based-component-)
7. [What are Pure Components and their purpose?](#what-are-pure-components-and-their-purpose-)
8. [What are Higher Order components?](#what-are-higher-order-components-)
9. [What HOCs have you used?](#what-hocs-have-you-used-)
10. [Have you used the Context API?](#have-you-used-the-context-api-)
11. [You already have state management in React, so why go for Redux?](#you-already-have-state-management-in-react-so-why-go-for-redux-)
12. [How does Redux work?](#how-does-redux-work-)
13. [Have you used any Middlewares?](#have-you-used-any-middlewares-)
14. [What is the purpose of using middlewares?](#what-is-the-purpose-of-using-middlewares-)

You can use these links to quickly navigate to each question in the document.

1. ### What is difference between useMemo and useCallback ?

`useMemo` is a React Hook that lets you cache the result of a calculation between re-renders.

```
const cachedValue = useMemo(calculateValue, dependencies)
```

`useCallback` is a React Hook that lets you cache a function definition between re-renders.

```
const cachedFn = useCallback(fn, dependencies)
```

In React, both `useMemo` and `useCallback` are hooks that are used to optimize performance by memoizing values and functions, respectively. They help avoid unnecessary re-computations and re-renders.

### `useMemo`:

`useMemo` is used to memoize the result of a computation (a value) and returns the memoized value. It takes two arguments: a function that computes the value, and an array of dependencies. The value is only recomputed when one of the dependencies changes.

```
import React, { useMemo } from 'react';

const MyComponent = ({ data }) => {
  const memoizedValue = useMemo(() => expensiveComputation(data), [data]);

  return <div>{memoizedValue}</div>;
};
```

In this example, `expensiveComputation` will only be called when the `data` dependency changes. The memoized value is stored and reused if the dependencies remain the same.

### `useCallback`:

`useCallback` is used to memoize a callback function. It returns the memoized function. Like `useMemo`, it takes a function and an array of dependencies. The memoized function is only recreated when one of the dependencies changes.

```
import React, { useCallback } from 'react';

const MyComponent = ({ onClick }) => {
  const memoizedCallback = useCallback(() => {
    // function implementation
    console.log('Button clicked!');
  }, []); // Empty dependency array means the callback will never change

  return <button onClick={memoizedCallback}>Click me</button>;
};
```

In this example, the `memoizedCallback` function will only be recreated if the dependencies change. This is useful in preventing unnecessary re-renders of child components that rely on this callback.

### When to Use Each:

- **`useMemo`:**
  - Use `useMemo` when you want to memoize the result of a computation (value) and only recalculate it when specific dependencies change.
  - Useful for optimizing the performance of computations that are not functions/callbacks.

- **`useCallback`:**
  - Use `useCallback` when you want to memoize a callback function and only recreate it when specific dependencies change.
  - Useful for optimizing the performance of callback functions, especially when passing them to child components, preventing unnecessary re-renders.

2. ### Explain Life Cycle Methods in class based components ?

In class-based components in React, the lifecycle of a component refers to the series of phases that a component goes through, from its creation to its removal from the DOM. The lifecycle methods are functions that are automatically called at different points during the existence of a component. Here are the main phases of the lifecycle in class-based components:

### Mounting:

1. **`constructor(props)` (optional):**
   - The constructor is called before a component is mounted. It is used to initialize state and bind event handlers.

2. **`static getDerivedStateFromProps(props, state)` (optional):**
   - A static method that is called just before rendering when new props or state are received. It is used to update the state based on the changes in props.

3. **`render()` (required):**
   - The `render` method is responsible for rendering the component's UI. It returns React elements.

4. **`componentDidMount()`:**
   - This method is called after the component has been rendered to the DOM. It is often used for tasks like data fetching, subscriptions, or setting up event listeners.

### Updating:

1. **`static getDerivedStateFromProps(props, state)` (optional):**
   - Similar to the mounting phase, this method is called just before rendering when new props or state are received. It is used to update the state based on changes in props.

2. **`shouldComponentUpdate(nextProps, nextState)` (optional):**
   - This method is called before rendering when new props or state are received. It returns a boolean indicating whether the component should re-render or not. It is used for performance optimization.

3. **`render()` (required):**
   - Same as in the mounting phase, the `render` method is responsible for rendering the component's UI.

4. **`getSnapshotBeforeUpdate(prevProps, prevState)` (optional):**
   - This method is called right before the changes from the virtual DOM are to be reflected in the actual DOM. It is used to capture information from the DOM before it potentially changes.

5. **`componentDidUpdate(prevProps, prevState, snapshot)` (optional):**
   - This method is called after the component has been updated in the DOM. It is often used for tasks like network requests, updating the DOM in response to prop or state changes, etc.

### Unmounting:

1. **`componentWillUnmount()`:**
   - This method is called before the component is removed from the DOM. It is used for cleanup tasks like canceling network requests, clearing up subscriptions, etc.

### Error Handling (Introduced in React 16):

1. **`static getDerivedStateFromError(error)` (optional):**
   - This method is called when there is an error during rendering. It is used to update the state to display a fallback UI.

2. **`componentDidCatch(error, info)` (optional):**
   - This method is called after an error has been thrown during rendering. It is used for logging the error information.

It's important to note that with the introduction of React Hooks in functional components and the `useEffect` hook, many of the lifecycle methods have equivalents for functional components. Class components are still valid, but functional components with hooks have become more common in modern React development.

![Lifecycle](https://github.com/saipavansiripuram/React-Interview-Questions/assets/69411783/43215d60-cd3f-426f-9eb3-78572dd5e053)



3. ### What hooks have you used?

I've used several React Hooks, including:
- `useState`: For managing state in functional components.
- `useEffect`: For handling side effects in functional components, similar to `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` in class components.
- `useContext`: For consuming values from the Context API within functional components.
- `useReducer`: For managing more complex state logic and actions in functional components.
- `useCallback`: For memoizing callback functions to prevent unnecessary re-renders.
- `useMemo`: For memoizing values to optimize performance.
- `useRef`: For accessing and interacting with the DOM or keeping mutable values between renders.

4. ### What is the purpose of useCallback?

`useCallback` is used to memoize a callback function in React. It returns a memoized version of the callback function that only changes if one of the dependencies has changed. The purpose is to optimize performance by preventing unnecessary re-creation of callback functions, especially in scenarios where these functions are passed as props to child components. This can help in avoiding unnecessary re-renders of child components when the parent component updates.

5. ### What are Class-based Lifecycle methods?

Class-based lifecycle methods are methods that are available in class components in React. They are invoked at different points in the lifecycle of a component, including mounting, updating, and unmounting. Some key class-based lifecycle methods include `componentDidMount`, `componentDidUpdate`, `componentWillUnmount`, and others. These methods allow developers to execute code at specific points in a component's existence.

6. ### How can you achieve componentDidMount, componentDidUpdate & componentDidUnMount in a functional-based component?

In functional components, you can achieve similar functionality to class-based lifecycle methods using the `useEffect` hook:
- `componentDidMount`: You can use `useEffect` with an empty dependency array to simulate the behavior of `componentDidMount`.
- `componentDidUpdate`: You can use `useEffect` with a dependency array to execute code when specific dependencies change, simulating the behavior of `componentDidUpdate`.
- `componentWillUnmount`: You can return a cleanup function inside `useEffect` to simulate the behavior of `componentWillUnmount`.

```javascript
import React, { useEffect } from 'react';

const MyComponent = () => {
  useEffect(() => {
    // componentDidMount logic
    return () => {
      // componentWillUnmount logic
    };
  }, []); // Empty dependency array for componentDidMount

  useEffect(() => {
    // componentDidUpdate logic
  }, [dependency]); // Dependency array for componentDidUpdate

  return <div>Functional Component</div>;
};
```

7. ### What are Pure Components and their purpose?

Pure Components are class components in React that extend the `React.PureComponent` class instead of the regular `React.Component` class. The purpose of Pure Components is to optimize performance by automatically implementing a `shouldComponentUpdate` method that performs a shallow comparison of props and state. If the props and state haven't changed, the component won't re-render, preventing unnecessary updates and potentially improving performance.

8. ### What are Higher Order components?

Higher Order Components (HOCs) are functions that take a component and return a new component with enhanced functionality. HOCs enable code reuse, logic abstraction, and the composition of multiple behaviors. They are commonly used for tasks like managing state, handling authentication, or adding specific functionalities to components without modifying their core logic.

9. ### What HOCs have you used?

I have used various HOCs, including libraries like `react-redux` that provide HOCs such as `connect` for integrating Redux with React components. Additionally, I have implemented custom HOCs for tasks like authentication, logging, and code reuse.

10. ### Have you used the Context API?

Yes, I have used the Context API in React. The Context API provides a way to pass data through the component tree without having to pass props manually at every level. It consists of the `React.createContext` function, `Context.Provider`, and `Context.Consumer`. It is particularly useful for sharing values like themes, authentication status, or language preferences across components.

11. ### You already have state management in React, so why go for Redux?

While React's built-in state management is suitable for managing local component state, Redux is a state management library that provides a centralized store to manage the global state of an application. Reasons to use Redux include:
- Managing complex state that needs to be shared across components.
- Predictable state changes with a unidirectional data flow.
- Time-travel debugging and state persistence with middleware like Redux DevTools.
- Middleware support for handling asynchronous actions.
- Easy integration with React components using the `react-redux` library.

12. ### How does Redux work?

Redux follows a unidirectional data flow. The flow involves:
1. **Action:** A plain JavaScript object that describes a change in the state. It must have a `type` property and can optionally carry payload data.
2. **Reducer:** A pure function that takes the current state and an action, and returns the next state. Reducers are combined to create the root reducer.
3. **Store:** An object that holds the state tree of the application. It has methods to dispatch actions and subscribe to state changes.
4. **Middleware:** Functions that can intercept and modify actions before they reach the reducer, or perform asynchronous tasks. Middleware enhances the functionality of Redux.

13. ### Have you used any Middlewares?

Yes, I have used middlewares in Redux to handle asynchronous actions, log actions, and integrate with external services. Popular middlewares include `redux-thunk` for handling asynchronous actions, `redux-logger` for logging actions, and custom middleware for specific application needs.

14. ### What is the purpose of using middlewares?

Middlewares in Redux provide a way to extend the capabilities of the store's dispatch function. Their purposes include:
- **Handling Asynchronous Actions:** Middleware like `redux-thunk` allows dispatching functions, enabling asynchronous logic in action creators.
- **Logging:** Middleware such as `redux-logger` can log each dispatched action and the resulting state changes.
- **API Integration:** Middleware can intercept actions, perform operations like making API requests, and dispatch new actions based on the results.
- **Enhancing Dispatch:** Middlewares can modify or enhance the dispatch function to add custom behavior before or after the action is processed by the reducers.

Middleware allows developers to extend and customize the behavior of Redux to suit the specific needs of an application.

