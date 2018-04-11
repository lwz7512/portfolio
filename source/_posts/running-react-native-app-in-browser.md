---
title: running react-native app in browser
date: 2018-04-08 21:28:46
tags:
---

## Background

RNA created by create-react-native-app command have great advantages in running on both iOS and Android platform, using the the same code infrastructure. Compared with native development process, the whole dev-lifecycle shorten greatly because of no-need of complete compilation, and hot deploy in device/simulator.

But these build process, based on packager and running on Expo client, looks like not satisfied and not much efficient as pure reactJS web development workflow. The FAMOUS problem is the ** Starting packager... ** bug in 'react-native-scripts'. It exists for more than half a year, and no further fix promoted. Besides, when the js file changed the device/simulator cannot update instantly and timely to see the new result, often need another modification to invoke hot deploy. It's frustrated.

So, I need a web solution to run react-native code in browser, and seeing the change result instantly and timely is a must. Then I found the ** [React Web](https://github.com/taobaofed/react-web) ** .


## How to

- first, create a blank reactjs project:

```
$ npm install -g create-react-app
$ create-react-app my-react-app

```

- then, install React Web

```
cd my-react-app
$ npm install --save react-web
```


- reinstall installed modules

If running 'npm start' in last step, react-scripts error would occur.
so, remove all the installed modules then install again:

```
$ rm -rf node_modules
$ npm install
```

- modify the index.js & App.js

Booting react-native component is slightly different from web, so, the index.js should make some changes:

index.js:

```
// add this
import {AppRegistry, Platform} from 'react-native';

// comment this two lines used for web merely
// ReactDOM.render(<App />, document.getElementById('root'));
// registerServiceWorker();


// also add these boot method used by native component
AppRegistry.registerComponent('App', () => App);

if (Platform.OS === 'web') {
  AppRegistry.runApplication('App', { rootTag: document.getElementById('root') });
}

```

App.js:

comment all the code originally used, then add below

```
import React, {Component} from 'react';
import {AppRegistry, StyleSheet, Text, View, Platform} from 'react-native';

class App extends Component {
  render() {
    return (
      <View style={styles.box}>
        <Text style={styles.text}>Hello, world!</Text>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  box: {padding: 10},
  text: {fontWeight: 'bold'}
});

export default App;

```

- now, it's time to start

```
$ npm start
```

the browser reopened localhost at port 3000, Hello world! successfully showed in screen. Made a change in App.js, then switch to browser, new result refreshed instantly.

That's my desired and familiar way!
