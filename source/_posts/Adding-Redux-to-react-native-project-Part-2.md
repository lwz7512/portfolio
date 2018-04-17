---
title: Adding Redux to react-native project Part 2
date: 2018-04-17 10:13:21
tags:
---

### Background

Last post we introduced Redux to a blank react-native project primarily. In this post we'll add Redux to a TODO list app, and also to implement a persistence feature to save added TODO item.

We borrow a well-written [TODO list app](http://www.reactnativeexpress.com/data_component_state) as a starting point, in this way we'll save a lot of energy to understand the mechanism of Redux.

### Preparation

To start refactoring, first we need to install Redux and redux-persist dependencies.

Adding belowing modules into package.json dependencies:

```
"react-redux": "^5.0.7",
"redux": "^3.7.2",
"redux-persist": "^5.9.1"
```

instead installation one by one, this time we install all in one command:

```
$ npm install
```

### Snippets

- Change index.js, add Redux, persistence, App component wrapper :

```
import { Provider } from 'react-redux';
import { PersistGate } from 'redux-persist/integration/react'

import App from './app/App';
import configureStore from './app/Redux';

const { store, persistor } = configureStore();

export default class Bootstrap extends Component {
    render() {
        return (
            <Provider store={store}>
                <PersistGate loading={null} persistor={persistor}>
                    <App/>
                </PersistGate>
            </Provider>
        );
    }
}

AppRegistry.registerComponent('AwesomeProject2', () => Bootstrap);
```
Last post we explained the reason why using Provider outside of App. This example we added a NEW ** PersistGate ** to wrap App, enable it to automaticlly save the state to device. The persistor is a new stuff introduced later.


- Change App.js, connect component to Redux, deliver data by dispatch action :

```
import { actionCreators } from './Redux'

onAddTodo = (text) => {
  // const {todos} = this.state
  // this.setState({
  //   todos: [text, ...todos],
  // })

  this.props.dispatch(actionCreators.add(text))
}

onRemoveTodo = (index) => {
  // const {todos} = this.state
  // this.setState({
  //   todos: todos.filter((todo, i) => i !== index),
  // })

  this.props.dispatch(actionCreators.remove(index))
}

```
As you have seen, the big changes to this component is the way it process data, rather than using setState it use ** props.dispatch() ** . Where doest it come? The answer is in connect function:
```
// inject app state from redux, then add new property todos to App component
const mapStateToProps = (state, ownProps) => ({
  todos: state.todos,
});

// Wrap App component with Connect component,
// and create interaction channel(props) for it.
const AppContainer = connect(
  mapStateToProps
)(App);

```

in mapStateToProps function App component obtained a new property named 'todos', how to use it?

```
render() {
  // const {todos} = this.state
  const {todos} = this.props

  return (
    <View>
      <Title>
        To-Do List
      </Title>
      <Input
        placeholder={'Type a todo, then hit enter!'}
        onSubmitEditing={this.onAddTodo}
      />
      <List
        list={todos}
        onPressItem={this.onRemoveTodo}
      />
    </View>
  )
}
```
Again, we don't use state anymore, using ** props ** instead!


- last, we have a look at new Redux.js

```
// Initial state of the store
const initialState = {
    todos: ['Click to remove', 'Learn React Native', 'Write Code', 'Ship App'],
}

// Helper functions to dispatch actions, optionally with payloads
export const actionCreators = {
    add: (item) => {
      return {type: 'ADD', payload: item}
    },
    remove: (index) => {
      return {type: 'REMOVE', payload: index}
    }
}
```

We seperate app state/data into Redux, so, initial data moved to here from App.js. Also, actions definded here for simplification.

last but not at least is the store creation function:

```
const _reducer = (state = initialState, action) => {
    // console.log(state);

    const {todos} = state;
    const {type, payload} = action;

    switch (action.type) {
        case 'ADD':
        return {
            todos: [payload, ...todos],
        }

        case 'REMOVE':
        return {
            todos: todos.filter((todo, i) => i !== payload),
        }

        default:
        // return default value while app start
        return state;
    }
};

// store.js
// with persistence support
export default function configureStore() {

    const persistedReducer = persistReducer(persistConfig, _reducer)

    const store = createStore(persistedReducer);
    let persistor = persistStore(store)

    return { store, persistor }
}

```

the big difference from the last post is that we use persistedReducer to create store, and a new stuff persistor created as the same time.

Remember the usage of persistor? It's used by PersistGate component in index.js.


So, that's the main points we need to notice in a persistenc enchanced Redux RNA. The complete source code for this app is in [here](https://github.com/lwz7512/AwesomeProject2)!

It can be used even in your daily life, isn't it?

Enjoy!
