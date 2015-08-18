---
title: Backbone and REST API
author: cadeorenie@gmail.com
categories: javascript
tags: backbone, node, rest, javascript
template: post
banner: img/post/backbone/post.jpg
date: 10/08/2015
---

Some months ago in my job we were discussing about which javascript frameworks would fit better to us. We selected some of them for testing and then, when I got to [Backbone], I realized it was a little bit different from the others. I won't get too deep about this on this text, maybe I publish a dedicated series about [Backbone] in the future.

Most part of the things I read was about Models, Collections and how it was awesome in [Backbone] when using a [Rest API][Rest]. The problem was I could not find a article show this as simples as it is.

So I'm here now, some time after, to do this. To show how beautiful this connection is.
	
### Show me some code!

*Note: this code can be [download on my Github](https://github.com/renie/backbone-node-sample "Go to github repo of this demo")*

This is actually an example for running in browser's console, so HTML file is just simple as that.

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8"/>
	<title>Document</title>
</head>
<body>
	<script src="https://code.jquery.com/jquery-2.1.4.min.js"></script>
	<script src="https://cdnjs.cloudflare.com/ajax/libs/underscore.js/1.8.3/underscore-min.js"></script>
	<script src="https://cdnjs.cloudflare.com/ajax/libs/backbone.js/1.2.1/backbone-min.js"></script>
	<script src="User.js"></script>
</body>
</html>
```

Until here nothing special, just importing [Backbone] itself and its dependencies ([jQuery] and [Underscore]). Just below these imports there is our example named 'User.js'.

So let's take a look to this User.js.

```javascript
var User = Backbone.Model.extend({
	urlRoot: '/users',
	idAttribute: '_id'
});

var Users = Backbone.Collection.extend({
	model: User,
	url: '/users'
});
```

*Note: this is just an example, avoid global variables as much as possible, PLEASE!*

Here we are just creating a [Backbone model](http://backbonejs.org/#Model "Go to documentation of Models in backbone"), defining what is our server URL for users and what property is coming in the return of this URL that represents the id of this object.

We are also creating a [Backbone collection](http://backbonejs.org/#Collection  "Go to documentation of Collections in backbone"), defining its model, so this will be a collection of users. And we are defining collection URL also.

I don't think it's worth to explain our [server file](https://github.com/renie/backbone-node-sample/blob/master/server.js "Directly link to server code of this demo") as the goal here is talk about [Backbone], but it's quite simple. Just a node server that serves a /users URL accepting GET, POST, PUT and DELETE methods, and a [minimalist database](https://github.com/louischatriot/nedb "Go to explanation about NEDB") for persisting data.

Now you can start trying things like this:

```javascript
var collection = new Users();

collection.fetch();
```

When you do this, [Backbone] will get the response below, convert to User objects and set as models of our collection.
```json
[
	{"name":"Carlos","age":90,"_id":"DSUhf9VvRuUrBQSP"},
	{"name":"Paula","age":55,"_id":"aRtYOIZn63xaybjy"},
	{"name":"Roberto","age":88,"_id":"pHYYwvcfizoMTW17"}
]

``` 

Then you can start using collection's models for doing operations as you want like:


```javascript
// delete Carlos
collection.findWhere({name: 'Carlos'}).destroy();

// update Paula
collection.findWhere({name: 'Paula'}).set('age', 20).save();

// create Alfred
var alfred = new User();

alfred.set('name', 'Alfred');
alfred.set('age', 35);

collection.add(alfred).save()
```

### Try it yourself!

[Download this on my Github](https://github.com/renie/backbone-node-sample "Go to github repo of this demo"), run **node server.js** and try it at **localhost:3000/getAll.html**. I'm sure you will understand it much better. It's very simple and can ease your start if you are starting with [Backbone].





[jQuery]: https://jquery.com/ "Go to jQuery official page"
[Underscore]: http://underscorejs.org/ "Go to Underscore official page"
[Backbone]: http://backbonejs.org/ "Go to Backbone official page"
[Rest]: https://en.wikipedia.org/wiki/Representational_state_transfer "Go to definition of REST on Wikipedia"