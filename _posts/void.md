---
title: Shoud I use void in my Javascript?
author: cadeorenie@gmail.com
categories: javascript
tags: javascript, void, undefined
template: post
banner: img/post/void/post.jpg
date: 22/09/2015
---

This is one of that things we use "because yes". But have you ever thought about void in Javascript? Do you know what is it used for? Ok, it's not a big deal, but here is the reason.

Void, in Javascript, is just an unary operator that returns **undefined** no matter what. So it can be used as a function, an expression can be passed, and it will return **undefined**. The most common example is:


```
<a href="javascript:void(0);"></a>
```

So href will call a javascript that will return **undefined**. In other words, in this case nothing happens.

As I said an expression would be valid, this is ok also?

```
<a href="javascript:void(alert('foo'));"></a>
```