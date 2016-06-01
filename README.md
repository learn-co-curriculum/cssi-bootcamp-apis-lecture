# Using APIs

SWBAT:
+ Understand the purpose of APIs
+ Get JSON data from an API by using the python requests library
+ Use an API Specific package.


## What is an API?

An API is short for Application Programming Interface. It's a way that developers can 'talk to' or interact with a variety of applications and software. For example, I want to programmatically place a pin on a Google Map. I shouldn't have to know exactly how to do this with javascript, html, and css. Instead, I can use Google's Maps API to make this happen and let Google's amazing internal engineering make the magic happen. APIs are amazing, because they allow us to tap in to the functionality of thousands of applications and integrate them into our own creations.

We're going to play with the Giphy API and create a little command line application that returns the slug and url of the first ten results of any search term.

## Making HTTPS requests in Python

### Step 1: Look at the API documentation

https://github.com/Giphy/GiphyAPI
Show that good APIs have good documentation. Generally you need an access token.
Have students take some time to find other cool APIs and share with the class.
Show students that APIs are just HTML requests by submitting a get request in the browser and showing them the big jumble of JSON that is received.

### Step 2: Create A Python File 
We're not going to be submitting our requests from the browser. Instead, we're going to do this programmatically. 


To do this, we need to install the 'requests' package using `pip install requests`. 
Create a new .py file called giphy_search.py and import the requests package.

```python
from google.appengine.api import urlfetch
import json

search_term = raw_input("Search term:").replace(' ', '+')
url = "http://api.giphy.com/v1/gifs/search?q={}&api_key=dc6zaTOxFJmzC&limit=10".format(search_term)

resp = urlfetch.fetch(url)

if resp.status_code != 200:
    # This means something went wrong.
    raise ApiError('resp.status_code')

for gif in json.loads(resp.content)["data"]:
    print('{} {}'.format(gif['slug'], gif['url']))
```

## Using a Package

https://github.com/shaunduncan/giphypop
