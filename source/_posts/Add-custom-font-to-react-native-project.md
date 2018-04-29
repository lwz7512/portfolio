---
title: Add custom font to react native project
date: 2018-04-29 18:23:50
tags:
---

### Background

In a recent RN project I'm working on, I need to display a handwriting chinese text in each card. But the default font library can not meet this demand, then, I searched a lot of reference and successfully completed it. It may look like complex, but the key steps are just a few, no much additional tricky parts!


### Snippets

Here, My sole mission is to install a font file named ** 'SentyMARUKO.ttf' ** to my project.

![](/img/SentyMARUKO.png)

to test the rightness, add the style definition:

```
bigText: {
    color: '#FFFFFF',
    fontSize: 64,
    fontFamily: 'SentyMARUKO',
},
```

then begin to change RN project:


- Step 1

make a folder named 'fonts' in project-root/app, to hold the SentyMARUKO.ttf

- Step 2

add below json snippt to package.json file:

```
"rnpm": {
    "assets": ["./app/fonts"]
  },
```

- Step 3

before run link command to install assets to ios/android project, install global rnpm first:

```
$ npm install rnpm -g
$ rnpm link
```

is it done? press CMD+r to see what'll happen....

![](/img/unrecognized_font.png)

Apparently not finished yet! The font resource installed to project but NOT automaticlly compiled to the running app. So, ** Unrecognized font family ...** error reported!

- Step 4

recomplie the project by running:

```
$ react-native run-ios
```

Note:

> KEEP dev server running background, do NOT close the console


this step ends up finishing the whole process of adding custom font to react native project.

Text with 'SentyMARUKO' font like this:

![](/img/note4kids_kong.png)

Compared with the original default Text font, look like much better?

![](/img/kong_default.png)
