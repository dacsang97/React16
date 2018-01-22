# Rewriting with React 16

## Problem No 1

> Adjacent JSX Tags should be wrapped with another parent element.

* React < 16

```jsx
render() {
    return (
        <button
            radius="4"
            className="couponBtn"
        >
            <span> Apply </span>
        </button>
        <span className="fieldWrapper">
            Buy Tickets
        </span>
    )
}
```

* **Solution**: Using React Fragments

```jsx
import React, { Fragment }  from "react";
render() {
    return (
        <Fragment>
            <button
                radius="4"
                className="couponBtn"
            >
            <span> Apply </span>
            </button>
            <span className="fieldWrapper">
                Buy Tickets
            </span>
        </Fragment>
    )
}
```

## Problem No: 2

> JavaScript errors inside components used to corrupt React’s internal state and cause it to emit cryptic errors on next renders.

* **Solution**: Use\_\_Error Boundaries
  > Error boundaries are React components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI instead of the crashed component tree.

A class component becomes an error boundary if it defines a new lifecycle method called componentDidCatch(error, info).

```jsx
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }
  componentDidCatch(error, info) {
    // Display fallback UI
    this.setState({ hasError: true });
    // You can also log the error to an error reporting service
    logErrorToMyService(error, info);
  }
  render() {
    if (this.state.hasError) {
      // You can render any custom fallback UI
      return <h1>Something went wrong.</h1>;
    }
    return this.props.children;
  }
}

<ErrorBoundary>
  <MyWidget />
</ErrorBoundary>;
```

* Messenger using Error Boundaries

!["Messenger using Error Boundaries"](https://i.imgur.com/ohtY5VU.png)

## Problem No 3

> Custom DOM Attributes

```html
<div boxname="test" />
    // will be displayed in React 15 as:
<div />
```

* **Solution:** With React 16, unknown attributes will be passed onto the DOM.

```html
<div boxname="test" />
// will be displayed in React 16 as:
<div boxname="test" />
```
