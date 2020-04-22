---
layout: post
title: "Security Series: CSRF Cross-Site Request Forgery"
date: 2020-01-03 06:00:00 -0700
categories: security, csrf, blog
---
![](/assets/img/pankaj-patel-u2Ru4QBXA5Q-unsplash.jpg){}

I previously described a SQL injection attack, and an XSS attack which is two of the main vulnerabilities on the web but
another vulnerability that is often missed is the Cross-Site Request Forgery attack (CSRF). 

A CSRF attack is when a malicious website sends a request to a web application where the user is already logged in and
authenticated.

For example, Sally was logged in to her credit union checking her balances for a purchase she wanted to make on online.
A quick search for the item she wants lands her on a questionable click-bait site which happens to be the malicious
site targeting Sally's credit union.

While Sally gets distracted reading the "10 reasons why you won't read all 10 reasons" article, the malicious site has
sent a post request via an iframe to the credit union transferring $100 to the attacker's account number. In this
scenario, the malicious website exploits the way the credit union's web application manages authentication.

One of the ways to protect against a CSRF attack is by checking that the referrer header is present and the referrer
is allowed. However, because ad blockers and privacy tools may strip the referrer header, this is not reliable.

Another way to protect against a CSRF attack is to use one-time-key tokens, session key, nonce or CSRF token.

Each link and form should have a token, this way if it is not present in the request then the request can be ignored
thus preventing a request forgery.

