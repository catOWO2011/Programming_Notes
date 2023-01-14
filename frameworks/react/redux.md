# Redux

# Content

| Subject |
|---------|
[What is Redux?](#what-is-redux) |
[State Management](#state-managment) |
[Redux Thunk](#redux-thunk)

## What is Redux
**Redux is a pattern and library for managing and updating application state, using events called "actions"**. It serves as a centralized store for state that needs to be across your entire application, with rules ensuring that the state can only updated in a predictable fashion.

## State Managment
In a self-contained app:
* The **state**, the source of truth that drives our app.
* The **view**, a declarative description of the UI based on the current state.
* The **actions**, the events that occur in the app based on user input, and trigger updates in the state.

## Redux Thunk
### What is a "thunk"?
The word `thunk` is a programming term that means "a piece of code that does some delayed work".

For Redux specifically, "thunks" are a pattern of writing functions with logic inside that can interact with a Redux store's dispatch and getState methods.

A thunk function is a function that accepts two arguments:

 * the Redux store `dispatch` method
 * the Redux store `getState` method

Thunk functions are not directly called by application code. Instead, they are passed to `store.dispatch()`.


