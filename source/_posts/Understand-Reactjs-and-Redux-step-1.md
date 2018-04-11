---
title: Understand Reactjs and Redux - step 1
date: 2018-04-11 23:01:47
tags:
---

### Background

Learning curve of reacjs & redux is absolutely steep, event for me, a senior front end programmar with years of experience. After a number of days of reading related official docs and examples officially recommended, I still feel frustrated and confused about those of conscepts and thoughts.

Then I met the minimal redux and even more simpler project to show how it could be. That helped me a lot to understand the usages and working flow in it.


### Reference

- [Minimal redux](https://redux-minimal.js.org/)

- [Super Simple React Redux Example
](http://blog.tylerbuchea.com/super-simple-react-redux-application-example/)


as well as the forked version of Super Simple React Redux Example, added with my comments in each function/concept.

- [My Simple React & Redux App](https://github.com/lwz7512/my-simple-app)


### Snipets

The most mysterious part in reactjs-redux for me is how do ACTION & REDUCER cooperate to produce STATE & PROPS change. So, I manage to figure something out there:

```
// AppContainer.js
// reducer -> state -> props
const mapStateToProps = (state, ownProps) => {
  console.log(state);
  // set geodP used in template above
  return {geodP: state.geodR};
};
```

this mapStateToProps function is common in redux, it accepts the state transfered from reducer function and produce the props object needed by ui element.

I modified the varaibles names, for example:

- Prop suffixed by capital character P.
- state value suffixed by capital character R means it is from reducers.

May be these are meaningless for a skilled reactjs coder, but currently it helped me to clearly identify the category of each stuff.


then another question came, where is the geodR in state from?


```
// redux.js
// state producer & exposer
export const reducers = combineReducers({
  // original: not easy to understand for beginner
  // geod,

  // redefined: expose geodR property for state using _geodR
  geodR: _geodR,
});

```

The anwser lies in reducers! It added a property called geodR to state and calculated the value by underscore prefixed geodR function for inner use. I believe this refactor is readability is better than the original version.


More understanding and clarification in code practice comming soon...
