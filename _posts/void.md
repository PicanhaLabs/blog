---
title: Shoud I use void in my Javascript?
author: cadeorenie@gmail.com
categories: javascript
tags: javascript, void, undefined, browser, ES5, ES3
template: post
banner: img/post/void/post.jpg
date: 22/09/2015
---

Have you ever thought about void in Javascript? Do you know what is it used for? Ok, it's not a big deal, but here is the reason.

Void, in Javascript, is just an unary operator that returns **undefined** no matter what. So it can be used as a function, an expression can be passed, and it will return **undefined**. The most common example is:


```
<a href="javascript:void(0);"></a>
```

So *href* will call a Javascript that will return **undefined**. In other words, in this case nothing happens.

As I said an expression would be valid, this is ok also:

```
<a href="javascript:void(alert('foo'));"></a>
```

### Why?

You could ask me:

> But if this returns **undefined**, why not use undefined instead?

Nowadays you can, not a problem.

![Back in my days, javascript was debugged with alert](../../../../img/post/void/back.jpg)

But some years ago, browsers used 3rd version of EcmaScript on its Javascript engines. And this version allowed to assign a new value to **undefined** variable. So this was possible:

```
window.undefined = true
```

Great, now undefined is true and you are in a debug hell.

Modern browsers doesn't have this problem, since this assignment is not allowed anymore. ES5 solved this mess.

But, just in case you have to support old browsers in your job, these are the list of browsers that allow this re-assign of undefined ([source](http://kangax.github.io/compat-table/es5/#Immutable_undefined)):

* Internet Explorer 8 and below;
* Firefox 3.6 and below;
* Android 4 and below;
* Safari 4 and below;
* Chrome 16 and below;
* Opera 12.5 and below;
* Konkeror 4.3 and below.

Some people say they use it instead of **undefined** because you use less chars. I really don't think this 2 characters, even it is being used a lot of times, will be a great gain but `¯\_(ツ)_/¯`.

### Is it used by someone?

Yeap, I believe that is just for compatibility reasons but same example of real world are:

* [Underscore](https://github.com/jashkenas/underscore/blob/master/underscore.js#L1325) : function for checking if a parameter is undefined (isUndefined());
* [Backbone](https://github.com/jashkenas/backbone/blob/master/backbone.js#L543) : function for clearing model attributes (clear());
* [ThreeJS](https://github.com/mrdoob/three.js/blob/master/build/three.min.js) : some minifiers change undefined for void 0, as you can see here

### Should I change my code and stop using undefined?

The most correctly answer would be: *Depends*. It depends on your browser support, and maybe on your concern about file size (really?).

But my anwser is: Ok, it depends, but probably you don't need to change. Nowadays it is more about your taste and maybe your project structure. But are not wrong using **undefined**, at all.