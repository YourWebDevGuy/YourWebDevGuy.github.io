---
layout: post
title: "Security Series: SQL Injections"
date: 2020-01-01 06:00:00 -0700
categories: security, sql, blog
---
![Earth Photo by NASA](/assets/img/nasa-Q1p7bh3SHj8-unsplash.jpg){:class="img-responsive"}

Although most of the hacks and data leaks you hear about now are due to misconfigurations of cloud services or weak
credentials, a few of the 'classic' vulnerabilities are still out on the web.

## SQL Injection

I have countless memories of SQL injection attacks that plagued the internet years ago. The reason why the SQL
injections were so common was that novice or careless programmers were building applications with PHP which was easy to
pick up, but also easy to make mistakes in when it came to security. 

Although PHP is the language everyone on the web tends to shudder at when they hear it, PHP is still one of the
dominating languages even today.

According to w3techs, PHP still owns almost 80% of the web market. This isn't a surprise as Wordpress, the world's most
popular blogging platform is built on PHP.

This is not to say PHP is a bad language. It is actually pretty powerful and in the hands of a competent developer,
you can do marvelous things. The matter of fact is that a SQL injection can occur in any programming language if we are
not careful.

Even in 2019 we still had some significant SQL Injection attacks which caused headaches for many organizations
including:

* **Oracle** (November 2019 - E-Business Suite PAYDAY vulnerability)
* **Cisco** (October 2019 - Unified Communications Manager) 
* **Amazon Alexa** (September 2019 - vulnerable to voice-based SQL Injection)
* **Sequalize** (September 2019 - ORM library vulnerable to SQL injection attacks)
* **Starbucks** (August 2019 - accounting database exposed)
* **MyCar** (August 2019 - cars exposed via remote apps)
* **Medical Informatics Engineering** (June 2019 - 3.5 million patient records exposed)
* **Epic Games** (January 2019 - All Fortnite player accounts exposed including credit card info)

SQL injection vulnerabilities can happen to an enterprise giant, your smart device at home, an npm library you may have
used at work, where you got your daily coffee, the handy mobile app in your car, where your doctor stored your personal
health information, or in the game you play at the end of a hard long day; vulnerabilities are everywhere and malicious
users are looking for a way to exploit any vulnerability they can find.

SQL is a declarative language where you ask the SQL Server for data. You can request data or modify it. You do not tell
the server how to retrieve it, but only what you need. Because of this the server receives a command and executes it.
The server does not know the intent of the command, so it executes the commands it receives.

SQL attacks vary by database engine (SQL Server, MySQL, Postgres, T-SQL, etc) but happen when working with dynamic SQL
statements. A dynamic statement is one that is generated at run-time with data from a form or query parameter.

Let's look at an example database with the following table:

A select query for the users table: `SELECT * FROM users`  returns three test records for alice, bob and charlie.

| id | username | email               |
|----|----------|---------------------|
|1   | alice    | alice@example.com   | 
|2   | bob      | bob@example.com     |
|3   | charlie  | charlie@example.com |

Imagine we have a simple form to look up a user by username:

![](/assets/img/empty_form.png){}

which  would return the result for bob along with an id and email:

| id | username | email               |
|----|----------|---------------------|
|2   | bob      | bob@example.com     | 

Behind the scenes we'd have the SQL statement: `SELECT * FROM users where username = "bob"` 


but if someone was trying to perform a SQL injection attack they could enter quotes into the form:

![](/assets/img/form_bob_quotes.png)

or even quotes with some additional SQL:

![](/assets/img/form_bob_sqli.png)

which would return the three test records in our database:

| id | username | email               |
|----|----------|---------------------|
|1   | alice    | alice@example.com   | 
|2   | bob      | bob@example.com     |
|3   | charlie  | charlie@example.com |

This happens because the SQL statement is being executed as-is. The database engine does not know if the statement is
malicious or not.



The statement can be read in two parts:

* `SELECT * FROM USERS WHEDDRE username = "bob"`: look for all users where the username is "bob"
* `or 1=1--`: return rows where something is always true. In this case, 1 is equal to 1 (don't eliminate rows)

A front-end developer may quickly point out that adding form validation and sanitizing before making a request can help
prevent sending the malicious data but this can be easily disabled by turning off javascript, injecting a similar form
without the validation, or even through a cross-site-scripting (XSS) attack.



The vulnerability is not limited to data from forms, it can also happen when making a request to a server where the
values from the request are used to lookup data in the database.



For example, the GET request to  `https://youtube.com/watch?v=123abc`  is fetching a video from the youtube database
with the id of `123abc`.

In a query parameter an attack could resemble a get request like the following: 

`https://mysecuresite.com/data?username=bob'+or+1=1--`

which would result in the query: `SELECT * FROM users WHERE username="bob" or 1=1--`

leading us back to the same vulnerability we looked at with the form example.

We would want to avoid someone using these injection attacks to steal data, change credentials or even drop entire
databases. What if the command would have been: `SELECT * FROM users where username = "bob"; drop database users`

A backend developer can also escape the values coming from the form or request. For example, in PHP 
the `mysql_real_escape_string` method is often used with a MySQL database to prepend backslashes to various characters
like quotes, semicolons, etc.

A more universal solution and a better approach to protect against SQL injection attacks are to use prepared statements.

In a prepared statement a question mark is used as a place holder for the data that will be used in the query.

`SELECT * FROM users where username = ?`

 Once received the data is escaped and the SQL injection vulnerability is resolved.