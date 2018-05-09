---
title: The right way to run react native audio example successfully
date: 2018-05-09 10:29:46
tags:
---

### Background

In my recent side RNA project 'AwesomeNote4Kids', I need to add a recording voice feature into it. Then [react-native-audio](https://github.com/jsierles/react-native-audio) module came to my viewport, it looks like a good option worthy of a try.

But after cloning the repository and installation of dependencies of AudioExample, I failed to successfully run the example in my Android phone, even if react-native link command executed. The Metro Bundler console reported  error:bundling failed: Error: Unable to resolve module `react` ...

The console gave the issue and resolve steps, I tried them several times, but still not worked. So, I have to stop and find a way out of this circumstance. May be a wholly new react native project worked?

### Snippets

first to init a new RN project by:

```
$ react-native init AudioExample
```

add two modules in dependencies to package.json:

```
"react-native-audio": "^4.1.3",
"react-native-sound": "^0.10.9"
```

then install them:

```
$ cd AudioExample
$ npm i
```

last but not at least, link the native code to the two platform build:

```
$ react-native link
```

By now, the project is ready to run smoothly, all we need to do is migrating the react-native-audio/AudioExample/`AudioExample.js` to `App.js`.

### Source Code

the complete `App.js` code is [here](https://github.com/lwz7512/AudioExample/blob/master/App.js)

After adding the permission to platform build, we can successfully run the project:

```
$ react-native run-android
```

complete project source code is [here](https://github.com/lwz7512/AudioExample)
