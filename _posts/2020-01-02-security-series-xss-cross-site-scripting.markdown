---
layout: post
title: "Security Series: XSS Cross Site Scripting"
date: 2020-01-02 06:00:00 -0700
categories: blog security xss
---
![](/assets/img/ilya-pavlov-OqtafYT5kTw-unsplash.jpg){}

I probably learned more about CSS by fiddling with my MySpace account in 2003 than I did during my web design class in
high school (a course where we only learned FrontPage and the magically generated nested-table code). 

<div style="text-align: center;">
<iframe allowfullscreen="" class="giphy-embed" frameborder="0" height="334" src="https://giphy.com/embed/DBa308wq8XTMs" width="480"></iframe></div>

It wasn't too long after MySpace was launched that one of the world's 'fastest-spreading virus of all time' was
unleashed with over one million users affected within the first few days. 
The virus was the result of an XSS or Cross-Site-Scripting attack.

The author of the webworm was a fella named Samy who was experimenting with a way to automatically grow his friend
count. The virus could have been malicious (exploiting vulnerabilities in IE to cause real damage) but luckily the
virus didn't do much more. Despite not being as evil as it could have been, MySpace had to temporarily shut down the
site in order to remove the worm. (also, Samy was charged with a felony by the government)

An XSS attack usually targets a user (not the website itself) this means the Samy virus didn't have to hack into the
MySpace servers in order to inject the virus. Instead, the XSS attack is either sent to a user through an email
containing malicious javascript or added to an unsecured web app through forms that lack validation and web pages
where the content served to the user is not properly escaped.

Through an XSS attack, an attacker can hijack an account, spread webworms, access browser history, access clipboard
data, control a web browser remotely and more.

Although an XSS attack is one of the most common types of attacks on vulnerable websites the solution for this is quite
simple:

All input should be validated and sanitized prior to sending it to the server.

All HTML output to the browser should be encoded to prevent the execution of javascript.

