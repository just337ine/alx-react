# 0x03. React Component

## Introduction

This README provides comprehensive details on various aspects of React components, including when to use class or functional components, the lifecycle of class components, testing components, utilizing Jest spies, understanding Higher-Order Components (HOCs), and optimizing performance in React applications.

## When to Use a Class or a Function to Create a Component

### Functional Components

Functional components are stateless and primarily used for simple, presentational logic. They are declared as functions and can use hooks (like `useState`, `useEffect`) for managing state and side effects.

**Use a functional component when:**

- You don't need to manage state or lifecycle methods.
- You prefer a simpler and more concise syntax.
- You want to leverage React hooks for state management and side effects.
- You aim for better performance and fewer complexities.

**Example:**

```jsx
const MyComponent = () => {
  return <div>Hello, World!</div>;
};
```

### Class Components

Class components are stateful and can utilize lifecycle methods. They are more feature-rich compared to functional components, especially before the introduction of hooks.

**Use a class component when:**

- You need to manage local state.
- You need to use lifecycle methods to control component behavior.
- You are working in a legacy codebase where class components are predominant.

**Example:**

```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      message: "Hello, World!",
    };
  }

  render() {
    return <div>{this.state.message}</div>;
  }
}
```

## The Lifecycle of a Class Component

Class components in React have several lifecycle methods that allow you to control the component's behavior during its creation, updating, and destruction phases.

### Mounting

- **constructor()**: Called when the component is initialized. Used to set up initial state and bind methods.
- **componentDidMount()**: Invoked immediately after the component is inserted into the DOM. Ideal for initiating network requests or subscriptions.

### Updating

- **shouldComponentUpdate(nextProps, nextState)**: Determines if a re-render is necessary. Returns `true` by default.
- **componentDidUpdate(prevProps, prevState)**: Called immediately after updating. Used to operate on the DOM or network requests after updates.

### Unmounting

- **componentWillUnmount()**: Called just before the component is removed from the DOM. Ideal for cleaning up subscriptions or timers.

### Error Handling

- **componentDidCatch(error, info)**: Called after an error has been thrown by a descendant component. Used for error logging and displaying fallback UI.

**Example Lifecycle Methods:**

```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  componentDidMount() {
    console.log("Component mounted");
  }

  shouldComponentUpdate(nextProps, nextState) {
    return nextState.count !== this.state.count;
  }

  componentDidUpdate(prevProps, prevState) {
    console.log("Component did update");
  }

  componentWillUnmount() {
    console.log("Component will unmount");
  }

  render() {
    return <div>{this.state.count}</div>;
  }
}
```

## How to Test a Component

Testing components ensures that they behave as expected. React components are typically tested using tools like Jest and React Testing Library.

### Setup

Install Jest and React Testing Library:

```sh
npm install --save-dev jest @testing-library/react
```

### Writing Tests

1. **Rendering**: Verify if the component renders correctly.
2. **Interaction**: Test user interactions like clicks and form submissions.
3. **State Changes**: Ensure state updates correctly based on interactions.

**Example Test:**

```jsx
import { render, screen, fireEvent } from "@testing-library/react";
import MyComponent from "./MyComponent";

test("renders the component", () => {
  render(<MyComponent />);
  expect(screen.getByText(/Hello, World!/i)).toBeInTheDocument();
});

test("increments counter on button click", () => {
  render(<MyComponent />);
  const button = screen.getByText(/Increment/i);
  fireEvent.click(button);
  expect(screen.getByText(/Count: 1/i)).toBeInTheDocument();
});
```

## How to Utilize a Jest Spy to Verify That a Function Is Being Called Correctly

Jest spies allow you to track calls to functions and verify their execution. This is particularly useful for ensuring that event handlers and callbacks are invoked as expected.

### Creating a Jest Spy

```jsx
import { render, screen, fireEvent } from "@testing-library/react";
import MyComponent from "./MyComponent";

test("calls the increment function on button click", () => {
  const incrementSpy = jest.spyOn(MyComponent.prototype, "increment");
  render(<MyComponent />);
  const button = screen.getByText(/Increment/i);
  fireEvent.click(button);
  expect(incrementSpy).toHaveBeenCalled();
  incrementSpy.mockRestore();
});
```

## What an HOC Is and How to Use It

### Higher-Order Component (HOC)

A Higher-Order Component is a function that takes a component and returns a new component. HOCs are used for reusing component logic.

**Use an HOC to:**

- Share common logic between multiple components.
- Enhance components with additional functionality (e.g., authentication, logging).

### Creating an HOC

```jsx
const withLogging = (WrappedComponent) => {
  return class extends React.Component {
    componentDidMount() {
      console.log("Component mounted");
    }

    render() {
      return <WrappedComponent {...this.props} />;
    }
  };
};

const MyComponentWithLogging = withLogging(MyComponent);
```

## How to Optimize Performance and Control Which Components to Render

### Performance Optimization Techniques

1. **Memoization**: Use `React.memo` for functional components and `PureComponent` for class components to prevent unnecessary re-renders.
2. **Lazy Loading**: Dynamically import components using `React.lazy` and `Suspense` to split code and reduce initial load time.
3. **UseCallback and UseMemo**: Optimize functions and values that depend on dependencies to avoid recreating them on every render.

**Example:**

```jsx
import React, { useMemo, useCallback } from "react";

const MyComponent = ({ items }) => {
  const computedItems = useMemo(() => {
    return items.map((item) => item * 2);
  }, [items]);

  const handleClick = useCallback(() => {
    console.log("Button clicked");
  }, []);

  return (
    <div>
      {computedItems.map((item, index) => (
        <div key={index}>{item}</div>
      ))}
      <button onClick={handleClick}>Click me</button>
    </div>
  );
};
```

### Conditional Rendering

Control which components render based on certain conditions using JavaScript logic.

**Example:**

```jsx
const MyComponent = ({ isLoggedIn }) => {
  return <div>{isLoggedIn ? <p>Welcome back!</p> : <p>Please log in.</p>}</div>;
};
```

## Resources

- [React Components](https://react.dev/reference/react/Component)
- [Enzyme Shallo](https://enzymejs.github.io/enzyme/docs/api/shallow.html)
- [Enzyme Mount](https://enzymejs.github.io/enzyme/docs/api/ReactWrapper/mount.html)
- [Enzyme Unmount](https://enzymejs.github.io/enzyme/docs/api/ReactWrapper/unmount.html)
- [React Pure components](https://legacy.reactjs.org/docs/react-api.html)
- [React Higher Order Components](https://legacy.reactjs.org/docs/higher-order-components.html)
- [Jest mock function](https://jestjs.io/docs/jest-object)
