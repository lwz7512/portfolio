---
title: Adding Redux to react-native project Part 1
date: 2018-04-15 21:10:24
tags:
---

### Background

After couples of days of learning, I believe I have understand the structure and concepts of Redux. Now it's time to put it into practice for a real react-native project. My goal is pretty simple: intergrating Redux to a react-native seed project by only ONE new source file added. In this way, everything is clear to overview and highlight the points.

### Boilerplate

To create a blank react-native project, I prefer to choose react-native cli rather than create-react-native-app! I'd tried the create-react-native-app & Expo, but I found that toolset might be problematic and inefficient to debug and restart a new dev server.

install react-native cli:

```
$ npm install -g react-native-cli
```

create a blank react-native project:

```
react-native init AwesomeNatiRedux
```

then, if we run 'react-native run-ios' or 'react-native run-android', we'll see the the Welcome screen in simulator or device(if Android device connected).


### Refactoring

Newly create react-native project code seems incompatible to Visual Studio Code 1.22.1. The editor complains the 'Props' only used in .ts file, so commented it and delete the <Props>.

My cli enviroment is:

```
$ react-native -v
react-native-cli: 2.0.1
react-native: 0.55.2
```

Opening the AwesomeNatiRedux folder in vs code, we'll see the two source file, index.js and App.js. One is entry file, another is root Component of the application.

Then, we'll begin to add Redux to the project step by step.


- Install redux dependency modules
```
$ npm install --save redux
$ npm install --save react-redux
$ npm install
```

now to test installation successful, just run: 'react-native start'.

- Change file structure
To make source file more reasonable and easily manage, we put all the source files into a app directory or src directory, left only index.js in the root of project. So mkdir app and move App.js to app directory. Besides, the redux logic file is going to be put the app directory.
```
$ mkdir app
$ mv App.js app/
```

- Change index.js
adding a bootstrap component to wrap App, and replacing the originally registered App component as root component:
```
// Add these imports - Step 1
import App from './app/App';
import { Provider } from 'react-redux';
import { store } from './app/redux';

export default class Bootstrap extends Component {
    render() {
        return (
            <Provider store={store}>
                <App />
            </Provider>
        );
    }
}

AppRegistry.registerComponent('AwesomeNatiRedux', () => Bootstrap);
```
in this file, we include the redux related component, Provider, to provide App level context for App component, while it just need a store to initiate.


- Create redux.js in app directory
the redux.js here includes 3 parts: actions/reducers/store which are indispensable to a Redux application.
In index.js above, we need store to reference, so it is exported:
```
export const store = configureStore();
```

- Refactoring the App.js
Why a react app need a Redux help, the answer can be very simple: to seperate or move the component level state to App level. The advantages are also obvious, easy to manage and share.
A modified version of App component may like this:
```
export class App extends Component {
  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.welcome}>
          {this.props.welcome}
        </Text>
        <Text style={styles.instructions}>
          {this.props.start}
        </Text>
        <Text style={styles.instructions}>
          {this.props.instructions}
        </Text>
        <Button
          onPress={()=>this.props.eventHandlerWithParam('Payload Sent!')}
          // onPress={this.props.eventHandlerNoParam}
          title="Learn More"
          color="#841584"
        />
      </View>
    );
  }
}
```

- Magic part:
Compared with the initial version of it, you'll find that state have been replaced to props, which means properties. How to achieve this?
Three function: mapStateToProps, mapDispatchToProps, connect.
```
// inject app state from redux
const mapStateToProps = (state, ownProps) => {
  console.log('new state Got!');
  // set properties from state
  return {
    welcome: state.welcome,
    start: state.start,
    instructions: state.instructions,
  };
};

// inject UI event handler from actions
// now got property activateGeodP & closeGeodP
const mapDispatchToProps = {
  eventHandlerWithParam: activateGeodX,
  eventHandlerNoParam: closeGeodX,
};

// Wrap App component with Connect component,
// and create interaction channel(props) for it.
const AppContainer = connect(
  mapStateToProps,
  mapDispatchToProps
)(App);

export default AppContainer;

```

that's the main refactoring process of react-native project to add Reduct support.

the complete project source code is [here](https://github.com/lwz7512/AwesomeNatiRedux).

Enjoy!
