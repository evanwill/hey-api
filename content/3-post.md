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
{% include card.md header="curl Reference" text=demo %}

# Text Processing API

[Text-processing.com](http://text-processing.com/) provides some basic natural language processing APIs designed for learning that are available without a key.
The APIs are based on Python [NLTK](https://www.nltk.org/) (see the [NLTK book](http://www.nltk.org/book/) for a great introduction to NLP and programming).
First, let's test out the [Sentiment Analysis service](http://text-processing.com/docs/sentiment.html).

{% include alert.md text='Sentiment analysis is an NLP method used to predict the subjective mood of text.
The model must be trained on existing annotated data, in this case online movie reviews which are an easy source of "labeled" data, and will provide probabilities the text would be categorized with various sentiments.
It will be most accurate for text that is similar to the training data, i.e. small chunks of modern English, *like a movie review*.' color="secondary" %}

Open a terminal and get ready to `curl`!
We need to use the data flag `-d` and the key `text` with the text we want to analyze as the value (less than 80,000 characters).
In response, we will get JSON data listing the sentiment probabilities and the most probable label (pos, neutral, or neg).
Your command should look like:

`curl -d "text=Something exciting and great." http://text-processing.com/api/sentiment/`

Optionally, we could pass another key value pair setting the language (english, dutch, or french).
You can combine the two key value pairs with `&`, or pass two `-d` parameters and curl will automatically concat them.

`curl -d "language=french" -d "text=tu es un très mauvais chien" http://text-processing.com/api/sentiment/`

Next, give the [Phrase Extraction & Named Entity Recognition service](http://text-processing.com/docs/phrases.html) a try:

`curl -d "text=The University of Idaho is located in Moscow" http://text-processing.com/api/phrases/`

# DBpedia Spotlight

[DBpedia Spotlight](https://www.dbpedia-spotlight.org/) is a web service to annotate text with linked open data entries from [DBpedia](https://wiki.dbpedia.org/about).
In this case, we aren't actually doing a POST request, but we need to use `curl` to pass along headers that tell the API what form of data to return.

For example, let's say we want to extract entities from this text and link them to DBpedia: "Moscow, Idaho is located in the Palouse near Pullman, Washington."
The API is at `https://api.dbpedia-spotlight.org/en/annotate` and we need to pass it the key `text`.

First, try pasting the GET URL into your browser:

`https://api.dbpedia-spotlight.org/en/annotate?text=Moscow, Idaho is located in the Palouse near Pullman, Washington.`

Notice the text value has spaces which need to be escaped with `%20`, but your browser is helpful and automatically does it for you!
The API has returned an HTML page, because the request came from a browser it assumes we want it in that form.
However, we may need another machine-readable format. 
The API will return `application/json`, `text/xml`, or `application/xhtml+xml` if we pass it as the `Accept` header in our request.
We can rewrite the query as a POST with headers asking for XML:

`curl -X POST -H "Accept:text/xml" -d "text=Moscow, Idaho is located in the Palouse near Pullman, Washington." https://api.dbpedia-spotlight.org/en/annotate`

We can add additional filters and parameters, such as limiting the type of entities extracted from the text:

`curl -X POST -H "Accept:application/xhtml+xml" -d "text=Moscow, Idaho was home to Carol Ryrie Brink and Josh Ritter." -d "types=Person,Organisation" https://api.dbpedia-spotlight.org/en/annotate`
