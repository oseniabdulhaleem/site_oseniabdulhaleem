---
title: "Security Practices I used on the backend during Tapha Development"
subtitle: ""
description: "Backend Security Practices"
date: 2024-06-22
author:      ""
image: ""
tags: ["software", "backend", "web-security", "tapha"]
categories: ["Software"]
---

/** Article Soon **/

/******\*\*******\*\*******\*\*******/

/******\*\*******\*\*******\*\*******/

/******\*\*******\*\*******\*\*******/

/** ARTICLE SOONNNNNNNNNN **/

/******\*\*******\*\*******\*\*******/

/******\*\*******\*\*******\*\*******/

/******\*\*******\*\*******\*\*******/

Some of the security practise i used are

- use of helmet for api security
- use of rate limiting on a 15 mins window
- secured cookies
- JWT
- CSRF applied to very important api route

- the use of http-only cookies for now and my plan to change it once it begins to scale

since it is served from a single heroku instance I've decided to stick to http-only cookies (perfect for the session state i'm handling) but it won't be able to scale as time goes on and more people use the platform
