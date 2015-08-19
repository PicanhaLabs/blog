---
title: Supporting older IE. What's your excuse?
author: cadeorenie@gmail.com
categories: opinion
tags: opinion, IE, excuses
template: post
banner: img/post/excuse-ie/post.jpg
date: 17/08/2015
---

Today I was watching a [talk](https://www.youtube.com/watch?v=XfZRsMkzVLM "Go to his talk (just in portuguese =/ )") of a [friend of mine](https://github.com/zigolis "Gabriel's Github") about front end architeture for high scalable systems. And in the beginning he talked, among other things, about why they support IE8-9.

Basically he used the most common argument for justifying their choice: *These IE versions represents good part of our company's gross sales.*

And this argument is not bad. You can say "but these companies are delaying web evolution" or "not even Microsoft support this version anymore". And you are not wrong. But you are arguing money with philosophy, and cannot convince CEO's with a beautiful history =(.

Otherwise you can always try to find a flaw in *money's argument*.


### The Calculation
** TL;DR : too lazy for this explanation? Jump to "After All section" and read Situation 1 **

First relation people try to use:

> We are an e-commerce and our gross sale is about 10 million/year. 10% of our users come from IE8. Therefore, ignore IE users will represent 1 million decrease in our revenues.

**Really?**, let's think about it.

This quote is assuming that every single user WILL buy something. If this really happens, congrats. This is probably the most successful e-commerce in history.

Then, it's saying every user spends the same money amount. It can happens, but how specific is this business?

I'm just saying: get real values so we can have a real discussion.

Let's assume that after that point we did an analysis and found the following data:

**Of these 10% of users using IE8, 50% buy something, and your expenses add up to 800k.**

Ok, now you could say:

> Well, 800k is still a good amount. It still justifies.

Caaalm down. Just hold this value.

Now you must to know how many hours you spent giving this support and what is the cost of this hours.

How many code is added to the project to support this browsers? Not just that little hack on css. I mean everything. Conditional Javascript, workarounds, polyfills, libraries included for not "reinvent the wheel". And now you can calculate how much storage you spend, how much you spend with data traffic. Depending on your architeture, if you don't load things on demand, do not forget measuring the perfomance decrease to other browsers for loading all this useless data.

Last but not least, try to measure (this is hard, but try), how many time did your team lost using an older solution for something that already has a better alternative nowadays, just because that old browser does not support.

Ok, here you can get all this amount of money and decrease from that 800k.

Ow, do not forget to decrease taxes also, as we are still talking about gross sales.

Here you have a REAL value to work. This is your real gain with this old browsers.

#### Indirect values

How many times did you hear this from coworkers?

> I feel trapped on this job. I want to create things but I can't because we have to support this or that browser.

And this guys (not judging if it's right or wrong) find another job that meets their expectations.

How many employees this company loses a year? And how many time(money) this company loses for training a new employee?


### After all

If even after this analysis the company decides to keep the support. Two situations:

1- This support really worth. Stop crying `¯\_(ツ)_/¯` .

2- The company doesn't give a shit for your calculation. So it's up to you. Keep your job, accept your reality and cry to the waiter in the end of the day. Or find a new one that fits your expectations.


### A Tip

If you are working as a freelance and your client said he NEEDS IEx(old versions, don't be lazy), use this technique: **Sir, this budget is for modern browsers. For this browser version the budget will be increased by 30% and for that version 70%.**

You are not cheating, you just are not absorbing the cost. And more, you are showing the cost of this work explicitly.

For my experience, in most of cases, this "NEED IEx" pass to "I think we can take care of this in the future, what you think?" in a minute ;).

Your client will want everything that is free.