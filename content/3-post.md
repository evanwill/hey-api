---
title: POST
nav: true
---

# POST

Many API services used to enhance data, such as geocoding or named entity recognition, use [HTTP POST](https://en.wikipedia.org/wiki/POST_(HTTP)) to transfer information to the server for processing.
A POST can be significantly more complex than GET, since it allows any amount of data to be attached to the body of the request.
This is also more secure than GET, since the information is encrypted in the message, rather than appended to the URL.

However, since this is not just a URL, to use this type of API we will have to create POST requests using a programming language, such as Python or Ruby. 
For testing, one of the best options is the command line tool [curl](https://curl.haxx.se/), which is installed by default on most Linux and Mac machines, and can be installed on Windows or used via Git Bash (from [Git for Windows](https://git-scm.com/)).

{% capture demo %}
- GET a website: `curl https://www.uidaho.edu`
- GET with more info: `curl -v https://www.uidaho.edu`
- Form data: `curl -F example=data https://example.com/form`
- POST with data: `curl -d "example stuff" https://example.com` (by default sent as "Content-Type: application/x-www-form-urlencoded")
- POST with headers: `curl -d '{"key":"value"}' -H 'Content-Type: application/json' -X POST https://example.com`
- POST using data file: `curl -d "@example.json" -X POST https://example.com`
- [curl POST docs](https://ec.haxx.se/http-post.html)
{% endcapture %}
{% include card.md header="Curl Reference" text=demo %}

# Text Processing API

[Text-processing.com](http://text-processing.com/) provides some basic natural language processing APIs available without a key, designed for learning.
The APIs are based on Python [NLTK](https://www.nltk.org/) (see the [NLTK book](http://www.nltk.org/book/) for a great introduction to NLP and programming).
First, let's test out the [Sentiment Analysis service](http://text-processing.com/docs/sentiment.html).

{% include alert.md text='Sentiment analysis is an NLP method used to predict the subjective mood of text.
The model must be trained on existing annotated data, in this case online movie reviews which are an easy source of "labeled" data, and will provide probabilities the text would be categorized with various sentiments.
It will be most accurate for text that is similar to the training data, i.e. small chunks of modern English, like a movie review.' %}

Open a terminal and get ready to curl!
We need to use the data flag `-d`, the key `text`, and the text we want to analyze as the value (less than 80,000 characters).
In response, we will get JSON data listing the sentiment probabilities and the most probable label (pos, neutral, or neg).
Your command should look like:

`curl -d "text=Something exciting and great." http://text-processing.com/api/sentiment/`

Optionally, we could pass another key value pair setting the language (english, dutch, or french).
You can combine the two key value pairs with `&`, or pass two `-d` parameters and curl will automatically concat them.

`curl -d "language=french" -d "text=Je vais bien" http://text-processing.com/api/sentiment/`

Next, give the [Phrase Extraction & Named Entity Recognition service](http://text-processing.com/docs/phrases.html) a try:

`curl -d "text=The University of Idaho is located in Moscow" http://text-processing.com/api/phrases/`


https://www.dbpedia-spotlight.org/api
