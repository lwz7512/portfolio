---
title: Understand Reactjs and Redux - step 2
date: 2018-04-12 12:00:39
tags:
---

### Background

Last post in step I explained the usage and principle of mapStateToProps function, also what's meaning for mapStateToProps to state and props. In a word, it's bridge to connect state to property used in UI template. Each time app state changed, component property changed also. So, the data flow as following:

> action --> reducer --> state --> property --> ui

all this thanks to mapStateToProps.


### Snipppets

In this post, I will describe another function named ** _mapDispatchToProps_ ** .

```
// Redefined version using p:x pair @2018/04/12
// bind action callback to component property
const mapDispatchToProps = {
  activateGeodP: activateGeodX,
  closeGeodP: closeGeodX,
};
// original version:
// const mapDispatchToProps = {
//   activateGeod,
//   closeGeod
// };

```

this function also returns a map for prop: action, with this map definition, the connected component abtained two additional properties to use:

- activateGeodP
- closeGeodP

the following image can prove it:

![](/img/react_con_with_dispatcher.png)

How does it happen? Nothing but the connect() function belowing:

```
// Wrap App component with Connect component,
// and create interaction channel(props) for it.
const AppContainer = connect(
  mapStateToProps,
  mapDispatchToProps
)(App);
```

What if we do not connect this ** _mapDispatchToProps_ ** to App? like this:

```
const AppContainer = connect(
  mapStateToProps,
  // mapDispatchToProps
)(App);

```

You may have guessed the result:

![](/img/react_con_no_dispatcher.png)


Yes, you got it! that's how do ** mapStateToProps ** and ** mapDispatchToProps ** work with connect function!


In the next few posts, I will continue to explore other concepts and building blocks that are must to understand for even the minimal reacjs apps.

keep tuning...
