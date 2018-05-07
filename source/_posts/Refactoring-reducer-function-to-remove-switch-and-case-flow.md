---
title: Refactoring reducer function to remove switch and case flow
date: 2018-05-07 13:45:08
tags:
---

### Background

Redux introduces reducer function to handle each action, and return new state data. It's a common usage to write a switch(action.type)/case workflow to process different action. This kind of measure leads to a very long and large reducer function, and mix all the scenarios together.

It's so ugly to accept, difficult to read and maintain. How to change this? In this post we'll simplify the reducer logic, and use as little code as possible to make it feel comfortable.

### Snippets

First, we define a struct names types which include all the action names:

```
const types = {
  ADD_ITEM: 'ADD',
  UPDATE_ITEM: 'UPDATE',
  SWITCH_ITEM: 'SWITCH',
  REMOVE_ITEM: 'REMOVE',
}
```

These constants definition is in global scope, defined once and referenced everywhere. we'll use them later in handler and reducer functions.

A typical reducer function use switch/case flow control to calculate new state by action. Any solution not to use switch sentence? Definitely! The answer is a ** map object ** like this:

```
let handlers = {
  [types.ADD_ITEM]:    hander_ADD,
  [types.UPDATE_ITEM]: hander_UPDATE,
  [types.SWITCH_ITEM]: hander_SWITCH,
  [types.REMOVE_ITEM]: hander_REMOVE
};
```

Compared with switch/case approach, is this implementation much easier to read? The greatest benefit of it is the action process is seperated from reducer, and redefined to a handler_xxx function.

Then, another problem come up, how to handler default action which's the initial state? The answer is just simple as well:

check existing action first, if not meet the action then return initial state!

```
const _reducer = (state = initialState(), action) => {
  let at = action.type;
  let handlers = {
    [types.ADD_ITEM]:    hander_ADD,
    [types.UPDATE_ITEM]: hander_UPDATE,
    [types.SWITCH_ITEM]: hander_SWITCH,
    [types.REMOVE_ITEM]: hander_REMOVE
  };

  if(handlers[at]) return handlers[at](state, action);

  return state;
};

```

 A sample handler function like this:


 ```
 const hander_REMOVE = (state, action) => {
   const {notes, index} = state;
   const {type, payload} = action; // from actionCreators

   return {
     notes: notes.filter((note, i) => i !== payload),
   }
 }
 ```

 Everything looks perfect! we achieved the goal of seperation of concern points.


the complete Redux.js code is [here](https://github.com/lwz7512/AwesomeNote4Kids/blob/master/app/Redux.js)!


...
