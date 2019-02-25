---
title: Intro
nav: true
---

# Web APIs

Application Program Interface (API)

recipes / contract / defined methods designed to make interaction with a server easier 

abstract way to interact with a server from outside using a web protocol (http) to get or submit data

this way you don't need to know the details about how the server works or the data is stored,
you can use any means to write the request,
server can use any means to respond,
but you communicate in a standardized way.
this allows the details of the user and the server to completely change without breaking the functionality.

[REST api](https://en.wikipedia.org/wiki/Representational_state_transfer)

other APIs 
- programming languages / libraries ([jQuery API](https://api.jquery.com/)
- Operating systems (POSIX, WinAPI)
- software features (browser api)

https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Client-side_web_APIs/Introduction

## How to find info

should be documented, otherwise its not a very good api...

In addition to formal documentation, information about alternative formats and search API are sometimes given in the `<head>` element of a web page. Check for `<link rel="alternate"`, `<link rel="search"`, or `<!--` comments which provide hints on how to interact with the site. These clues provide a recipe book for interacting with the server using public links.
