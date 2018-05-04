---
title: Create form with tcomb-form-native
date: 2018-05-04 21:11:38
tags:
---

### Background

HTML element has built-in form component , but no corresponding part for react-native. So, we have to do some additional work wrapping some basic component to create a form component. Then, some of excellent third part form components won the developers' star in reactjs community. One of the best is ** [tcomb-form-native](https://github.com/gcanti/tcomb-form-native) ** . Today, we'll use this component to create a simple form, and display it in a popup modal.

### Snippets

install the form component module is just as simple as the below command:

```
$ npm install tcomb-form-native --save
```

after installation, the two module included in package.json:

```
"redux-persist": "^5.9.1",
"tcomb-form-native": "^0.6.11"
```

In the Example section of the tcomb-form-native README.md, it use require function to reference the library, but we can also use ES6 ** import ** for uniformity to other basic react-native component import.

```
// var t = require('tcomb-form-native');
import t from 'tcomb-form-native';
```

After that, we have a Form ** Class ** from the t:

```
const Form = t.form.Form;
```

Now, we are ready to create a real Form instance by combining three parts:

- domain model, a struct to define your form fields;
- form options, an object to define the relevant visual/invisible attributes about fields;
- Form tag, the visual part returned in render function;


the complete implementation code like this:

```
var Card = t.struct({
  big: t.String,              // a required string
  title: t.maybe(t.String),  // an optional string
  subtitle: t.maybe(t.String),  // an optional string
  // age: t.Number,               // a required number
});

var options = {
  fields: {
    big: {
      label: '词汇', // <= label for the name field
      placeholder: '填写你要记忆的词汇'
    },
    title: {
      label: '解释',
      placeholder: '填写对该词汇的解释'
    },
    subtitle: {
      label: '举例',
      placeholder: '对该词汇造句或者相关词汇'
    }
  }
}; // optional rendering options (see documentation)

...

<Form
  ref="form"
  type={Card}
  options={options}
  value={this.state.value}
/>

...
```

what does it look like? here it is:

![](/img/form.png)


the end result of the component source code is in [here](https://github.com/lwz7512/AwesomeNote4Kids/blob/master/app/components/ModalForm.js)!

next post we'll figure out how to dynamically create a popup form rather than defined in the root view of app component.

coming soon...
