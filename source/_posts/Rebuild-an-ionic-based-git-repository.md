---
title: Rebuild an ionic based git repository
date: 2018-05-10 14:41:35
tags:
---


### Background

Yesterday my colleague submitted an ionic project to github, my task is to use the repository to package a Android & ios installation file.  But after I cloned the repository, running `cordova prepare` in console, it reported:

> Error: Current working directory is not a Cordova-based project.

what?

I searched many results and tried the solutions, but still the same error! I had to figure out what's the difference of this repository and the blank new ionic2 project.

### Snippets

to create a blank new ionic2 project, run:

```
$ ionic start blanknewio2 --v2 --ts
```

Compared with the local blank new ionic2 project, a `www` directory not existed in cloned project:

![](/img/ionic2.png)


The answer is clear now, www directory is ignored and not committed! By checking the `.gitignore` file in both projects, `www/` is included in without any unexpected.

So, mannually create a www directory then rerun the installation commands:

```
$ mkdir www
$ cordova prepare
$ npm i
```

now, it's ready to build ionic app source to each platform :


```
$ ionic build android --prod
$ ionic build ios --prod
```

DONE!
