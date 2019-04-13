---
title: GET
nav: true
---

# GET

The simplest forms of APIs use the [HTTP GET method](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods), essentially utilizing URL patterns to request information from a server.
With GET requests, your query is encoded in the URL string, thus limited in length (2048 ASCII characters), complexity, and security.

We can demo using these APIs simply by constructing the URL following the recipe, then pasting it into a web browser. 
However, combining these methods with a scripting language such as Python or tool such as OpenRefine can make them very powerful.

{% capture example %}
Let's say you had a list of IDs for a set of YouTube videos. 
You can use the YouTube img API to get thumbnails (this is no longer officially documented and is replaced by the more complicated [YouTube Data API](https://developers.google.com/youtube/v3/)).

Plug each ID into the URL pattern `https://img.youtube.com/vi/` + ID + `/0.jpg`.
For example, the ID `SWVjQsvQocA`, will look like `https://img.youtube.com/vi/SWVjQsvQocA/0.jpg`.
Also, try other format options `/0.jpg` through `/3.jpg`, `/hqdefault.jpg`, `/mqdefault.jpg`, and `/maxresdefault.jpg` for different sizes and thumbs.
Use your scripting language or OpenRefine to build the pattern with each ID and request the thumbnails as a batch.
{% endcapture %}
{% include card.md text=example title="For Example..." %}

APIs should be well documented, otherwise its not a very good api...
In addition to formal documentation provided by the service, information about alternative formats and search API are sometimes given in the `<head>` element of a web page. 
Check for `<link rel="alternate"`, `<link rel="search"`, or `<!--` comments which provide hints on how to interact with the site.

# IIIF

[International Image Interoperability Framework (IIIF)](https://iiif.io/) is an effort to standardize methods to access images and annotations from repositories.
The API standard was created by a collaborative community so that software developers can create compliant viewers and image servers, enabling better user and developer experiences across many platforms.

Let's look at the [IIIF Image API](https://iiif.io/api/image/2.1/) to learn how to request an image. 

IIIF URI syntax looks like:

`{scheme}://{server}{/prefix}/{identifier}/{region}/{size}/{rotation}/{quality}.{format}`

Each parameter has standard options or syntax, gradually building up the exact specifications of the image you want.

For example, let's use IIIF to access images from the [Psychiana](https://digital.lib.uidaho.edu/digital/collection/psychiana/search) digital collection hosted on [CONTENTdm](https://www.oclc.org/en/contentdm.html).

Base of the recipe:

- Our IIIF service is at the base URL `https://cdm17254.contentdm.oclc.org/digital/iiif`
- The collection name is the "prefix", `/psychiana`
- One item, ["Photograph of clerical and bookkeeping staff from the branch mailing department"](https://digital.lib.uidaho.edu/digital/collection/psychiana/id/548/rec/1), has the "identifier", `548`

First, get image info: 

`https://cdm17254.contentdm.oclc.org/digital/iiif/psychiana/548/info.json`

Get max size:

`https://cdm17254.contentdm.oclc.org/digital/iiif/psychiana/548/full/max/0/default.jpg`

Scale down to 50%:

`https://cdm17254.contentdm.oclc.org/digital/iiif/psychiana/548/full/pct:50/0/default.jpg`

Get a cropped region:

`https://cdm17254.contentdm.oclc.org/digital/iiif/psychiana/548/125,125,250,250/max/0/default.jpg`

# Chronicling America

The [Chronicling America](https://chroniclingamerica.loc.gov/) project provides access to millions of pages of digitized historic newspapers.
It also includes a simple, open API to interact with the repository programmatically.
Unlike the IIIF which is a standard, this API is custom built into the repository system and is used by its own web pages to retrieve data.
Read the [documentation](https://chroniclingamerica.loc.gov/about/api/) to learn how to build URL queries.

To search individual pages, the recipe is:

- base URL, `https://chroniclingamerica.loc.gov`
- service location, `/search/pages/results`
- query string using the [search parameters](https://chroniclingamerica.loc.gov/search/pages/opensearch.xml) and selecting a format, `?key=value&key=value&format=json`

Let's build up an example query string:

- from Idaho, `state=Idaho`
- from the years 1865 to 1866, `date1=1865&date2=1866&dateFilterType=yearRange`
- only the front pages, `sequence=1`
- sorting by date, `sort=date`
- returning a maximum of five, `rows=5`
- in JSON, `format=json`

Combine the parameters with `&` and let's see what we get:

<https://chroniclingamerica.loc.gov/search/pages/results?state=Idaho&date1=1865&date2=1866&dateFilterType=yearRange&sequence=1&sort=date&rows=5&format=json>

After retrieving a batch of data, we could parse the JSON to analyze or use it to form a new batch of queries.

{% include alert.md text="If ChronAm seems interesting, try out the [Library of Congress JSON API](https://libraryofcongress.github.io/data-exploration/index.html) or [LOC IIIF API](https://github.com/LibraryOfCongress/data-exploration/blob/master/IIIF.ipynb)." align="center" color="success" %}

# Other simple APIs to try

Some free, GET APIs:

- Fandom: [PokéAPI](https://pokeapi.co/) or [Star Wars API](https://swapi.co/)
- Trivia questions: [jService](http://jservice.io/) or [Open Trivia Database](https://opentdb.com/api_config.php)
- [Fun Translations API](https://funtranslations.com/api)
- [NumbersAPI](http://numbersapi.com/)
- [ip2country](https://ip2country.info/)
- [Geocode.xyz](https://geocode.xyz/api)
