---
title: Quick Notes
date: 2018-03-10 14:40:51
---

What did you learn yesterday?
====================================


## 2017/12/26

- Reinstall windows10 home edition by usb iso:

http://joshbe         am.com/2017/11/23/making-a-bootable-windows-10-usb-drive-on-macos-high-sierra/

$ diskutil list
$ diskutil eraseDisk MS-DOS "WINDOWS10" MBR disk#
$ cp -rp /Volumes/CCCOMA_X64FRE_EN-US_DV9/* /Volumes/WINDOWS10/


- Reslove partition format problem during installation:

press Shift+F10 to open dos window, then...

- Convert harddisk format from MBR to GPT in MS-Dos:

> diskpart
DISKPART > list disk
DISKPART > select disk 0
DISKPART > clean
DISKPART > convert gpt
DISKPART > create partition primary size = 40960
DISKPART > format fs=ntfs quick
DISKPART > exit



## 2017/12/27

- verdaccio

Lightweight private npm proxy registry

$ npm install --global verdaccio
$ npm set registry http://localhost:4873
$ npm adduser --registry http://localhost:4873



## 2017/12/28

- Graceful degradation versus Progressive enhancement

https://www.w3.org/wiki/Graceful_degradation_versus_progressive_enhancement

development approaches

Graceful degradation: alternative version to make sure the usability.
Progressive enhancement: improved version by usability basline.

- Difference:

Gd start high, whereas Pe start extensive.
Gd try to fix, Pe try to pre-consideration.
Gd looking back, Pe looking forward.


## 2017/12/29



## 2017/12/30



## 2018/01/03

- Promise.resolve(value)

returns a Promise object that is resolved with the given value.
> If the value is a thenable (i.e. has a "then" method), the returned promise will "follow" that thenable
> if the value was a promise, that object becomes the result of the call to Promise.resolve;


## ...


## 2018/01/05

- npm_lazy

http://mixu.net/npm_lazy/

npm can be slow, down or return random errors if you have large deploys
npm_lazy caches packages on your local network, making things faster and more predictable


## 2018/01/07

- mochajs

https://mochajs.org/#getting-started

assert, describe(),
$ ./node_modules/mocha/bin/mocha

test script in package.json

"scripts": {
    "test": "mocha"
}

run the test with:

$ npm test


## 2018/01/08

- PRPL pattern

https://developers.google.com/web/fundamentals/performance/prpl-pattern/

PRPL is a pattern for structuring and serving Progressive Web Apps (PWAs),
with an emphasis on the performance of app delivery and launch. It stands for:

> Push critical resources for the initial URL route.
> Render initial route.
> Pre-cache remaining routes.
> Lazy-load and create remaining routes on demand.


- DEMO:
https://shop.polymer-project.org/

- SOURCE:
https://github.com/Polymer/shop


## 2018/01/09

- <commit-ish>

Indicates a commit or tag object name.
A command that takes a <commit-ish> argument ultimately wants to operate on a <commit> object
but automatically dereferences <tag> objects that point at a <commit>.


## 2018/01/10

- for...in vs for...of

推荐在循环对象属性的时候，使用for...in,在遍历数组的时候的时候使用for...of。

for...in循环出的是key，for...of循环出的是value

注意，for...of是ES6新引入的特性。修复了ES5引入的for...in的不足

for...of不能循环普通的对象，需要通过和Object.keys()搭配使用


## 2018/01/13

the principles behind the CDN:


CDN目的是通过在现有的Internet中增加一层新的网络架构，将网站的内容发布到最接近用户的网络“边缘”，
使用户可以就近取得所需的内容，解决 Internet 网络拥塞状况，提高用户访问网站的响应速度。
CDN是一种组合技术，其中包括源站、缓存服务器、智能DNS、客户端等几个重要部分。

客户资源请求 --> 智能DNS --> 缓存服务器 <-- 源站

A content delivery network or content distribution network (CDN) is a geographically distributed network
 of proxy servers and their data centers. The goal is to distribute service spatially relative to
 end-users to provide high availability and high performance.


## 2018/01/15

- hexo plugin development workflow
- hexo-admin plugin custom development workflow
- Meteor.js disable send enrollment email, and Meteorjs package structure



## 2018/01/16

- javascript source map

https://blog.rapid7.com/2017/05/24/what-are-javascript-source-maps/

Source maps create a map from these compressed asset files back to the source files.
This source map allows you to debug and view the source code of your compressed assets,
as if you were actually working with the original CSS and Javascript source code.

- install tool:

$ npm install uglify-js -g

- generate

$ uglify-js file1.js file2.js -o output.js --source-map output.map.js


- bind()

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind




## 2018/01/17

```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

## 2018/01/18

- TLS VS SSL ?

- APNs push server needed port: 2695, 2696, 443

- HTTP/2

https://http2.github.io/
https://http2.github.io/faq/


The focus of the protocol is on performance; specifically,
end-user perceived latency, network and server resource usage.
One major goal is to allow the use of a single connection from browsers to a Web site.

- What are the key differences to HTTP/1.x?

At a high level, HTTP/2:

 - is binary, instead of textual
 - is fully multiplexed, instead of ordered and blocking
 - can therefore use one connection for parallelism
 - uses header compression to reduce overhead
 - allows servers to “push” responses proactively into client caches



$ nslookup gateway.push.apple.com



## 2018/01/19


```
# order by date:
$ ls -als  
```

Apache config:

- DocumentRoot has root configuaration in global httpd.conf
- VirtualHost DocumentRoot must under DocumentRoot directory defined in httpd.conf
- Using Alias can map specific context to some directory under DocumentRoot
- Static files hosting can coexist with reverse proxy in the same config
- http config using 80 port, https config using 443 port


## 2018/01/23

using nohup & exit to keep program running in background

$ nohup ./start.sh &
$ exit


## 2018/01/26

- RESOLVE git problem while pushing: shallow update not allowed

As it seems you have used git clone --depth <number> to clone your local version.
This results in a shallow clone. One limitation of such a clone is that you can't push from it into a new repository.

This means that you have to unshallow your repository.
To do so you will need to add your old remote again.

$ git remote add old <path-to-old-remote>
$ git fetch --unshallow old

And now you should be able to push into your new remote repository.



## 2018/01/28

- understanding save() and restore() for the canvas context

context.save() pushes the current state onto the stack,
context.restore() pops the top state one the stack, restoring the context to that state.

save and restore can be used as a solution to a wide variety of situations.
one of the most common uses is for transformations.

- javascript Array.slice() vs Array.splice()

slice get the children of array, whereas splice change the children of array

splice example:

// remove first
this.drawWords.splice(0,1)
// insert to the first
reorderedArray.splice(0, 0, uDiscover)


## 2018/02/01

- javascript string to lower case:

str.toLowerCase()


## 2018/02/06

official doc:
https://facebook.github.io/react/docs/reusable-components.html#es6-classes

blog:
http://cheng.logdown.com/posts/2015/09/29/converting-es5-react-to-es6


difference between constructor and getInitialState in reactjs

ES6 classe:
```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {  };
  }
}
```
is equivalent to ES5:
```
var MyComponent = React.createClass({
  getInitialState() {
     <!-- initial state  -->
    return {  };
  },
```
- ES6 The Spread Operator

...xx : expands an array into individual parameters when using the dots in a function call

```
let attr = {a: 1, b: 2, c: 3};
let props = {d: 4, ...attr};
console.log(props);

{a: 1, b: 2, c: 3, d:4}

```

## 2018/02/23

http://bluebirdjs.com/docs/getting-started.html

bluebird




## 2018/03/10

- Pug, originally jade lang

https://github.com/pugjs/pug

- javascript string trim from end

var str = "12345.00";
str = str.substring(0, str.length - 1); // "12345.0"

This is the accepted answer, but as per the conversations below,
the slice syntax is much clearer:

var str = "12345.00";
str = str.slice(0, -1); // "12345.0"


## ...




## ...




## ...




## ...




## ...
