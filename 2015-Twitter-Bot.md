# Brief

Project link: https://twitter.com/alpha3po

This was for a [hackathon](https://twitter.com/iamyoursumit/status/655285176637849600) that we made in 24 hours. 

# Goal 
Alert people about disasters

# How it worked?

1. Using regular expressions and Twitter tweets we were able to make a bot, which could check all the tweets which matched a certain keyword. 

2. In our case, we wanted to get all the tweets that matched: "earthquake" AND "magnitude"

3. Once the tweets were captured the bot would take the text and tweet them back.


# Stack:

>##  v0.0

Initially, we planned to do it as a web-app. 

People could open the link and there would be categories of disasters for e.g., Earthquakes would be a category

**Frontend**:

> Stack: Bootstrap + AJAX:

Hardest problems and lessons learnt?

### Problem 

**SPA with MVC Architecture:** We were using MVC architecture, but wanted to do this as a single page application. We needed to do some additional tweaks to accomplish that.

### Solution: 

1. Used pure AJAX to make requests to the backend.

```
const Http = new XMLHttpRequest();
const url='https://jsonplaceholder.typicode.com/posts';
Http.open("GET", url);
Http.send();

Http.onreadystatechange = (e) => {
  console.log(Http.responseText)
}
```

2. We checked the route url to see what current page we were at for e.g.,  https://dismap.com/earthquakes, would return current category as earthquake.

3. Changed the location url using history push state

```
window.history.pushState({"html":response.html,"pageTitle":response.pageTitle},"", urlPath);
```

### Problem

**Twitter API Limits**: Twitter API has limits so before making queries we had to keep checking whether we hit it or not.

### Solution

1. Wrote a backend API for checking what the current limits were

2. Before making a request from the frontend, the API would be hit.

**Backend**:

> Stack: Ruby-on-Rails

### Problem

Integrating with Twitter API, managing oauth tokens.

### Solution

1. Wasn't a particularly hard problem, but our work around for this was to use .env variables

2. Added .env to .gitignore for security reasons.

### Problem

Despite our strict filter for certain keywords, we ran into tweets which were unrelated to our goal. 

### Solution

1. We upgraded our filters to only select tweets when units of measurement of the disaster were mentioned.

Simple example would be:
```
const regex = RegExp('(richter)|(mph)');

console.log(regex.test(str));
```


>## v1.0

We realized no one would visit the website, since most people were already on Twitter. So we decided to make it a bot, which would post real-time updates

> Stack: Tweepy

### Problem

Switch from a webapp to a bot + run the service 24x7

### Solution

1. Scratched the frontend, backend. 

2. Extracted the API functions for getting data and filtering. Some manual tweaks to make it work on python. Luckily, there was a good library called Tweepy which allowed for transition.

3. One of the main problems with this approach was deployment. Heroku was our go to option for webapp, but did heroku support standalone bots?

4. After some research we figured out we needed to write an endpoint for the Twitter API to authenticate, so we made the API on `web.py`.

5. Deployed the app on heroku and changed the Twitter AUTH url.

6. Hardest problems here was in **deployment**, consuming the data and tweeting weren't really a problem.
