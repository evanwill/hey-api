---
title: Intro
nav: true
---

# Web APIs

Web Application Program Interfaces (APIs) are defined methods designed to make interaction with a server easier--think of them as recipes or contracts.
They provide an abstract way to interact with a server from outside using a web protocol (http) to request or submit data.

This layer of abstraction is important because:

- you can use any means to make the request if it follows a standard protocol (http)
- you don't need to know the details about how the server works or how the data is stored
- the server can use any means to respond

**If you communicate in the standardized way defined by the API, it allows the details of both the user and the server to completely change without breaking the functionality.**

plug in picture

[REST api](https://en.wikipedia.org/wiki/Representational_state_transfer)

Other APIs

- programming languages / libraries ([jQuery API](https://api.jquery.com/)
- Operating systems (POSIX, WinAPI)
- software features (browser api)

https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Client-side_web_APIs/Introduction

## How to find info

should be documented, otherwise its not a very good api...

In addition to formal documentation, information about alternative formats and search API are sometimes given in the `<head>` element of a web page. Check for `<link rel="alternate"`, `<link rel="search"`, or `<!--` comments which provide hints on how to interact with the site. These clues provide a recipe book for interacting with the server using public links.
