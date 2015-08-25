---
title: Backbone and REST API Part 2 - Server
author: cadeorenie@gmail.com
categories: javascript
tags: backbone, node, rest, javascript
template: post
banner: img/post/backbone2/post.jpg
date: 20/08/2015
draft: true
---

As I promised on the [first post][FirstPost], this is a post to explain the server side of that [Backbone] sample with [Rest API][Rest].

Actually, as I told there, it's pretty simple: just starting a server, listening on a specific port, waiting for some HTTP methods and persist on a very small database. Let's see this step by step and then the whole file.

### First the first stuff

First part, requiring dependencies:

```javascript
var express     = require('express'),
    bodyParser  = require('body-parser'),
    DataStore   = require('nedb'),
    app         = express(),
    http_port   = 3000,
    usersDb     = new DataStore({filename:'users.nedb'});
```

Here we are calling a micro web framework called [Express] for helping on mapping urls and HTTP methods. Then we use [body-parser] to format our requests. [NEDB], our little database.

After those requires, we create an instance of [Express], choose a port, and load the base **users.nedb**.

```javascript
app.use(express.static(__dirname + '/src'));
app.use(bodyParser());
```
Now we just config our static directory to **src** and ask [Express] to use [body-parser].

OK, we are ready to start our mappings!

### URL Mappings

**Express** URL mapping use the following syntax:

```javascript
app.[HTTP_METHOD]([URL], [What will happen0]);
```

So the first mapping is:

```javascript
app.get('/users', function(req, res) {
    // logic for getting our users from database
});
```

Very simple, isn't it?

Ok, now you want to receive a get parameter. Not a problem, you can see this on the second mapped URL.

```javascript
app.get('/users/:user_id', function(req, res) {
    var id = req.params.user_id;
});
```

You just have to say that this URL will receive a parameter via **:param_name**, and get this on attribute **params** of **request**.

After doing your stuff, in this case just get data from database, you have respond to your requester. And this is made using the method **send** of **response**. Just like this:

```javascript
app.get('/users', function(req, res) {
    res.send({
        'my' :'data'
    });
});
```

Knowing all this, you can now implement your **POST**, **PUT** and **DELETE**.

### Finishing...

Now just start the server and be happy!

```javascript
app.listen(http_port);
```

*Note: this full code can be [viwed and downloaded on my Github](https://github.com/renie/backbone-node-sample/blob/master/server.js "Go to github repo of this demo")*


[Backbone]: http://backbonejs.org/ "Go to Backbone official page"
[Rest]: https://en.wikipedia.org/wiki/Representational_state_transfer "Go to definition of REST on Wikipedia"
[FirstPost]: /2015/08/10/backbone-and-rest-api "Go to first post"
[Express]: http://expressjs.com/ "Go to Express official page"
[Body-Parser]: https://www.npmjs.com/package/body-parser "Go to body-parser page on NPM"
[NEDB]: https://github.com/louischatriot/nedb "Go to NEDB page on Github"