# `lit-redux`

`lit-redux` is implementation of [`react-redux` API](https://github.com/reactjs/react-redux) for [`lit-html`](https://github.com/PolymerLabs/lit-html) library.

## Example

```js
import {html, render} from 'lit-html/lib/lit-extended';
import {connect} from 'lit-redux';
import {createStore, bindActionCreators} from 'redux';

const todos = (state = [], action) => {
  switch (action.type) {
    case 'ADD_TODO':
      return state.concat([action.text]);
    default:
      return state;
  }
};

const store = createStore(todos, ['Use Redux']);

const actions = {
  add() {
    return {
      type: 'ADD_TODO',
      text: `Hello ${Math.random()}`
    };
  },
};

const todosView = connect(
  state => ({ todos: state }),
  dispatch => ({ actions: bindActionCreators(actions, dispatch) })
)(({todos, actions}) => html`
  ${ todos.map(text => html`<p>${ text }</p>`) }
  <button type="button" onclick="${ () => actions.add() }">Add</button>
`);
  
render(
  html`${ todosView({ store }) }`,
  document.body
);
```

[Live Demo](https://codepen.io/alex_maslakov/pen/RjKJNo?editors=1000)

## Current progress

* Implemented `connect()` function (only `storeKey` option is available)

## Other related projects

* [`lit-html`](https://github.com/PolymerLabs/lit-html) - `lit-html` lets you write HTML templates with JavaScript template literals, and efficiently render and re-render those templates to DOM
* [`lit-form`](https://github.com/jmas/lit-form) - Formik API implementation for `lit-html` library
* [`lit-todo-example`](https://github.com/jmas/lit-todo-example) - `lit-html` + `lit-redux` + `lit-form`
