---
title: stuck at Starting packager...
date: 2018-04-06 21:54:23
tags:
---

Recently I started to learn react-native app development from zero. Reactjs/react-native has emerging for couples of years, and growing to a very big and mature ecosystem. I had given a glimpse to it, but can not be accustomed with JSX way to mingle script/template/style into one file. As an AngularJS/Ionic developer for almost 4 years, I gradually realized the limitation of the Ionic/Cordova approach. So, I began to step into reactive world this year.

After several days of official reactjs/react-native documentation reading, I start to create my first react-native app. Things changed a lot since the first publish of react-native, now it recommends to use ** create-react-native-app ** to start a RNA.

- install create-react-native-app globally

```
$ npm install -g create-react-native-app

```
- create rn-app with create-react-native-app cli

```
$ create-react-native-app rn-my-app
```

- install Expo client in mobile phone to preview your RNA

  [Expo official site](https://expo.io/tools)

- enter app dir and start dev server

```
$ cd rn-my-app
$ npm start
```

less than 20 seconds, you will the the following the output in console:

 ```
 > rn-my-app@0.1.0 start /Users/username/mobile/rn-my-app
 > react-native-scripts start

 22:40:00: Starting packager...
 Packager started!



A BIG QR CODE IMAGE HERE



 Your app is now running at URL: exp://192.168.1.103:19000

 View your app with live reloading:

   Android device:
     -> Point the Expo app to the QR code above.
        (You'll find the QR scanner on the Projects tab of the app.)
   iOS device:
     -> Press s to email/text the app URL to your phone.
   Emulator:
     -> Press a (Android) or i (iOS) to start an emulator.

 Your phone will need to be on the same local network as this computer.
 For links to install the Expo app, please visit https://expo.io.

 Logs from serving your app will appear here. Press Ctrl+C at any time to stop.

  › Press a to open Android device or emulator, or i to open iOS emulator.
  › Press s to send the app URL to your phone number or email address
  › Press q to display QR code.
  › Press r to restart packager, or R to restart packager and clear cache.
  › Press d to toggle development mode. (current mode: development)


 ```

I tried to use Expo app installed in my Android mobile to scan the QR code, but nothing happened. Then I press `a` in console, the application showed in screen(my Mac connected to mobile by usb cable).

To see the modified result of the app, just made some changes in App.js then waiting for rebuilding process and new content will present in the screen.

It looks like easy and smooth, everything is OK until I press Ctrl+c to shutdown the dev server.

> When I attempted to restart the packager by ** npm start --reset-cache ** , it stopped in Starting packager...

even waited for couples of minutes, NO further progress AT ALL!!!

Then ctrl+c an restart again repeatedly and repeatedly... no changes.

...


It made me almost crazy for this, the build server can't start again and development process stopped there also. So, there is no choice but to turn to search engine, finally, I found the post:

> Stuck in "Starting packager"

> https://github.com/react-community/create-react-native-app/issues/203

and this:

> react-native-scripts start stuck at "Starting packager..."

> https://github.com/react-community/create-react-native-app/issues/343


The key solution is the watchman tool to kill all the file monitor process, then would be successful restart.

so, install watchman first:

```
$ brew update
$ brew install watchman
```

then, executing the watchman delete & shutdown command, console print the clear result:

 ```
 [username@~] $ watchman watch-del-all && watchman shutdown-server
{
    "version": "4.9.0",
    "roots": [
        "/Users/username/mobile/rn-my-app"
    ]
}
{
    "version": "4.9.0",
    "shutdown-server": true
}
 ```
  

 last, executing the restart command in app root:

 ```
[liwenzhi@~/mobile/rn-my-app] $ npm start --reset-cache
 ```

14 seconds later, the Packager started!
