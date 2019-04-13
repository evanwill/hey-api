---
title: Intro
nav: true
---

# Web APIs

Server-side Web Application Program Interfaces (APIs) are defined methods designed to make interaction with a server easier--think of them as recipes or contracts, where if you provide the expected input you will receive an expected output.
Web APIs provide an abstract way to interact with a server from the outside using a web protocol (http) to request or submit data.

This layer of abstraction is important because:

- you can use any means to construct the request (so long as it results in an http request)
- you don't need to know the details about how the server works or how the data is stored
- the server can use any means to respond (so long as it results in an http response)

{% include alert.md text="**If you communicate in the standardized way defined by the API, it allows the details of both the user and the server to completely change without breaking the functionality.**" color="primary" %}

{% capture plugs %}
Think about the outlets in your house.
Any device with the standard plug can be connected to the socket and receives the standardized amount of power. 
You do not need to know anything about the power generation or electrical grid that delivers it to your house (other than paying the bill). 
Likewise, the utility company doesn't need to know what you are plugging in, it just delivers the expected voltage.
This makes the interaction considerably simpler--you do not need to rig up custom wiring and voltage regulators for every device.
{% endcapture %}
{% include card.md text=plugs title="For Example..." img="rawpixel-1061399-unsplash.jpg" alt="power strip and plugs" %}

# Other APIs

This workshop uses the term "server-side web APIs" to refer to services exposed on the web via a well documented set of HTTP requests.
Sometimes called "third party APIs" when used in web pages, they might involve asking for specific data from a repository or sending a text sample to be processed in the cloud.

However, API is a generic term that is used in many different programming contexts, generally "a set of clearly defined methods of communication among various components" ([API, Wikipedia](https://en.wikipedia.org/wiki/Application_programming_interface)).
For example:

- Programming languages and libraries ([jQuery API](https://api.jquery.com/))
- Operating systems ([POSIX](https://en.wikipedia.org/wiki/POSIX), [WinAPI](https://en.wikipedia.org/wiki/Windows_API))
- Software features (Browser APIs)

**Web/Browser APIs**, *confusingly* also often called "Web APIs", are programming interfaces built into web browsers that allow client-side JavaScript (i.e. code in web pages) to interact with their features. Sometimes called the Browser Object Model (BOM), they include APIs such as the [Document Object Model (DOM)](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction) and Device APIs (Ambient Light Sensor, Geolocation, Screen Orientation). See the MDN [Web APIs list](https://developer.mozilla.org/en-US/docs/Web/API).
