---
title: Why another static generator?
author: cadeorenie@gmail.com
categories: javascript
tags: node, javascript, static, generator
template: post
banner: img/post/backbone/post.jpg
date: 31/08/2015
draft: true
---

For those who maybe asking: there are so many static generator tools, why making another?! Here is your answer.

When Gabriel and I decided to make this blog the requirement were: We want a static website, 'cause it is cheaper for hosting as we don't need a complex server or a database.

Our first option was [Jekyll](http://jekyllrb.com/). We already used it on other project, so why not use it? Well, we unfortunately all of our team, besides me, uses Windows. And we all know that working with Ruby or Python on Windows is not a bed of roses. And beyond this, for using Pygments on Windows you cannot use the lastest version. For making *watch* command work on Windows you need another stuff. So we don't want this.

Second option was [Hexo](https://hexo.io/). Very nice tool, just node, great. So I start to search for something related with i18n on Hexo, and found a lot of issues, some closed and some still opened. Very long discussion. 

So I tried to use this feature. I don't if documentation is too bad, or it's a buggy feature, or this too hard to use. The fact is: it didn't work. 

Another problem was [this](https://github.com/hexojs/hexo/issues/1263). Issues in chinese/english. I know there are people that doesn't know english. I'm not a native english speaker also (far from this). But if you can do this in english, easier for most part of community, why not?

Then we start seeking for a node tool. We program Javascript, best option for us, and it works on Unix-like and Windows. And we found a lot of options, but they were outdate, or nobody commits on this since 2013, or bugs everywhere.

At this point, Gabriel told me:

> Why don't we create a generator?

At first I'm like: **hmmm, I don't know. Create from zero...**. Actually I was lazy about this. But then, this friend start the project, I changed my mind and we are here =).

Now we have our 1.0 version. It's beginning, just basics for now, but we really want to make this happen. We have a lot of ideas, but sure community is always welcome. And this blog is built on this tool we made, so we can easily check every bugs reported.

So [check our project out](https://github.com/PicanhaLabs/PicanhaJS), fork us and help us making this better and better.


Thank you!

