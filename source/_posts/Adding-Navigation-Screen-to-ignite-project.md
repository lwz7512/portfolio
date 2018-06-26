---
title: Adding Navigation Screen to ignite project
date: 2018-06-26 21:50:03
tags:
---

### Background

The first time of usage of ignite cli and boilerplate are early May. As I was a beginner of RN and it seemed too complex for me at that time, so I gave up. But after a complete zero to release building of my first RNC, I'm familiar with the work flow and the project structure than ever. So, today I went back the iginite project and did some experiments in it. The biggest gain in this exercise is the usage of `react-navigation` and `react-native-navbar`.

### Snippets

first install iginite cli:

```
$ npm install -g ignite-cli
```

then create a iginite based react-native app:

```
$ ignite new PizzaApp
```

> Choose Andross when prompted, react-native-vector-icons needed also
> DevScreens is not required here

Default PizzaApp has only one screen `LaunchScreen`, but I want to add another screen, and implement navigation from LaunchScreen to new screen.

create new screen with cli:

```
$ ignite generate screen PizzaLocationList
```

then, two file appeared in project:

```
PizzaApp/App/Containers/PizzaLocationListScreen.js
PizzaApp/App/Containers/Styles/PizzaLocationListScreenStyle.js
```

one file modified:

```
PizzaApp/App/Navigation/AppNavigation.js
```

added a new line in StackNavigator:

```
PizzaLocationListScreen: { screen: PizzaLocationListScreen },
```

this defined a new router path, the name is `PizzaLocationListScreen`.

Now, time to add navigation button in LaunchScreen, add belowing into the ScrollView of LaunchScreen rendered view:

```
<Button
  title="Go to Pizza List"
  onPress={() => this.props.navigation.navigate('PizzaLocationListScreen')}
/>
```

see that? the name in navigate() is new router name we have defined.

Now, let's run it to see what will happen...

```
$ react-native run-ios
```

when we press the button `Go to Pizza List`, forward new screen, but..... CAN NOT GO BACK !!!

How to do with?

Adding a navigation bar certainly.

install `react-native-navbar` by :

```
$ yarn add react-native-navbar
```

then import to `PizzaLocationListScreen`

```
import NavigationBar from 'react-native-navbar';
```

adding this component into rendered view of PizzaLocationListScreen:

```
<View style={styles.mainContainer}>
  <NavigationBar
    title={titleConfig}
    leftButton={backIconBtn}
  />
  <ScrollView style={styles.container}>
    <KeyboardAvoidingView behavior='position'>
      <Text>PizzaLocationListScreen</Text>
    </KeyboardAvoidingView>
  </ScrollView>
</View>
```

ok, that's the go back NavigationBar customed by `titleConfig` and `backIconBtn` element.


### Screenshots

![ignite-navigation](/img/ignite_nav.png)

### Source code

[is here](https://github.com/lwz7512/PizzaApp)


...
