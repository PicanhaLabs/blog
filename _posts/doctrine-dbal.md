---
title: Doctrine 2 - DBAL
author: gaba.alan@gmail.com
categories: php
tags: doctrine, php, dbal, database
template: post
banner: img/post/backbone/post.jpg
date: 28/09/2015
---

Some days ago I was on a research about an ORM to use in our system.

So I remembered about Doctrine, because I already had other experiences with this ORM and it was good.

But before entering on this, I want to bring you Doctrine's DBAL (Database Abstraction Layer).

First, we must know that an ORM (Object-Relational Mapping) can exists without a DBAL. But, by obvious reasons, **its always good to have a DBAL** to abstract the diferences between database engines.

So, lets start configuring the DBAL. I'll use composer PHP to manage dependencies, but you can manage it by yourself.

Put the dependency of Doctrine DBAL, at **composer.json**:

```json
{
    "require": {
        "doctrine/dbal": "2.5.1"
    }
}
```

Then run the below command:

```
php composer.phar install
```

Doing that we have the dependencies installed, and we can create the bootstrap.php that contains a DBAL configuration. **botstrap.php** must create a connection with these database parameters:

```php
<?php
// bootstrap.php
require_once "vendor/autoload.php";

$config = new \Doctrine\DBAL\Configuration();

$connectionParams = array(
    'driver'   => 'pdo_pgsql',
    'host'     => 'localhost',
    'user'     => 'postgres',
    'password' => 'YOUR_PASSWORD',
    'dbname'   => 'postgres',
);

$conn = \Doctrine\DBAL\DriverManager::getConnection($connectionParams, $config);
```

I'm using the PostgreSQL database, but you can use other one like MySQL, SQL Server or Oracle. Let's use that connection created by bootstrap.php:

```php
<?php
// index.php
require_once 'bootstrap.php';

$stmt = $conn->query('select * from products');
$result = $stmt->fetchAll();

foreach( $result as $row ) {
	echo $row['name'] . '<br/>';
}
```

Here we have a simple SQL that selects all fields of PRODUCTS table and print product names.

The query method is the most simple one for fetching data, but it also has several drawbacks:

* There is no way to add dynamic parameters to the SQL query without modifying $sql itself. This can easily lead to a category of security holes called SQL injection, where someone can modify the SQL executed or even execute their own queries through clever exploiting of the security hole;
* Quoting dynamic parameters for a SQL query is tedious work and requires lots of use of the Doctrine\DBAL\Connection#quote() method, which makes the original SQL query hard to read/understand.
* Databases optimize SQL queries before they are executed. Using the query method you will trigger the optimization process over and over again, although it could re-use this information easily using a technique called **prepared statements**.

This three arguments and some more technical details hopefully convinced you to investigate prepared statements for accessing your database.

#### Prepared Statements

Consider the previous query, now parameterized to fetch only a single article by id. Using ext/mysql (still the primary choice of MySQL access for many developers) you had to escape every value passed into the query using mysql_real_escape_string() to avoid SQL injection:

```php
<?php
$sql = "SELECT * FROM articles WHERE id = '" . mysql_real_escape_string($id, $link) . "'";
$rs = mysql_query($sql);
```

If you start adding more and more parameters to a query (for example in UPDATE or INSERT statements) this approach might lead to complex to maintain SQL queries. Prepared statements separate these two concepts by requiring the developer to add **placeholders** to the SQL query. Placeholders in prepared statements are either simple positional question marks **(?)** or named labels starting with a double-colon **(:name1)**. You cannot mix the positional and the named approach. The approach using question marks is called positional, because the values are bound in order from left to right to any question mark found in the previously prepared SQL query. That is why you specify the position of the variable to bind into the bindValue() method:

```php
<?php
$sql = "SELECT * FROM products WHERE id = ?";
$stmt = $conn->prepare($sql);
$stmt->bindValue(1, $id);
$stmt->execute();

//Named parameters have the advantage that their labels can be re-used and only need to be bound once:
$sql = "SELECT * FROM users WHERE name = :name OR username = :name";
$stmt = $conn->prepare($sql);
$stmt->bindValue("name", $name);
$stmt->execute();
```
Doctrine 2 has some others ways to retrieve data, and it can be useful in some cases. **You can see them [here](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/data-retrieval-and-manipulation.html).**

But I want to write more about others methods implemented by Doctrine DBAL. Inserts, Updates and Deletes.
You might be thinking that I'll show you how to write SQL's like 'UPDATE table...' or 'DELETE FROM table...'. **But I don't.**

Doctrine has three simple methods that abstract: insert, delete and update:

```php
<?php
$conn->delete('user', array('id' => 1));
// DELETE FROM user WHERE id = ? (1)

$conn->insert('user', array('username' => 'jwage'));
// INSERT INTO user (username) VALUES (?) (jwage)

$conn->update('user', array('username' => 'jwage'), array('id' => 1));
// UPDATE user (username) VALUES (?) WHERE id = ? (jwage, 1)
```

**By default Doctrine DBAL does no escaping**. Escaping is a very tricky business to do automatically, therefore there is none by default. The ORM internally escapes all your values, because it has lots of metadata available about the current context. When you use standalone Doctrine DBAL, you have to take care of this by yourself. The following methods can help you with it:

```php
<?php
$quoted = $conn->quote('value');
$quoted = $conn->quote('1234', \PDO::PARAM_INT);
```

Maybe I have not impressed you with that DBAL, or you had others good experiences on another DBAL libs, but I want to tell you about one last thing: **SQL Query Builder**.

Doctrine 2.1 ships a powerful query builder for SQL language. This QueryBuilder object has methods to add parts to a SQL statement. If you build the complete state you can execute it using the connection it was generated from. The API is roughly the same as that of the DQL Query Builder, which we'll talk about in other moment.

You can access the QueryBuilder by calling Doctrine\DBAL\Connection#createQueryBuilder:

```php
<?php
$conn = DriverManager::getConnection(array(/*..*/));
$queryBuilder = $conn->createQueryBuilder();
```

It is important to understand how the query builder works in terms of preventing SQL injection. Because SQL allows expressions in almost every clause and position the Doctrine QueryBuilder can only prevent SQL injections for calls to the methods setFirstResult() and setMaxResults().

All the other methods cannot distinguish between a user and a developer input.

To safely work with QueryBuilder you should NEVER pass a user input directly to any of the methods of QueryBuilder and use the placeholder ? or :name syntax in combination with $queryBuilder->setParameter($placeholder, $value) instead.

Here an simple example of Query Builder:

```php
<?php
$queryBuilder
    ->select('id', 'name')
    ->from('users')
    ->where('email = ?')
    ->setParameter(0, $userInputEmail)
;
```

So, thats enough for today. Next post we will talk about Doctrine 2 ORM, which is one of the best PHP ORM's.

Until then.


[Doctrine]: http://www.doctrine-project.org/ "Go to Doctrine official page"
[Doctrine DBAL]: http://www.doctrine-project.org/projects/dbal.html "Go to Doctrine DBAL page"