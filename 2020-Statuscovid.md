# Brief

Coronavirus prep is a single page website that I made for getting an understanding of the coronavirus situation. Since, there are so many blogs and related information about this topic, but people who wanted to understand what the virus was and how to effectively prevent it quickly were missing. With this app you can minimize the time to understand coronavirus and maximize the likelihood of understanding how to prevent and transmit it further. There is also a timeline on the growth rate on a day to day basis for the residents of India.  The project was built from scratch by me using Next.js and some external APIs.


## Problem
Getting data from reliable sources

## Solution

1. To get real-time data, was consuming John Hopkins API. 

2. The problem with John Hopkins API was, they were consuming from multiple clients internally.

3. Wasn't a documented API, was one of the many internal services they were using. Had to inspect the network calls then extract which calls got the data.

4. Checking which request got the data, some requests would duplicate results and have some unique values. Had to make sure there were no repetitions on merging data from multiple sources.

```
Array.prototype.unique = function() {
    var a = this.concat();
    for(var i=0; i<a.length; ++i) {
        for(var j=i+1; j<a.length; ++j) {
            if(a[i] === a[j])
                a.splice(j--, 1);
        }
    }
    return a;
};

```


## Problem
Setting up all the data in a single page

## Solution

1. This was a more of a design problem rather than technical problem.

2. How do you show all the data for a disease, while making sure itsn't too overwhelming for the visitor.

3. Way to solve this was using `flex`

```
.grid {
  display: flex;
}
```


## Problem
Getting country specific data

## Solution
1. When you visit the website, you want to get more data where you are living.

2. Didn't want to ask for "location" for the user. 

3. Decided to use IP of the visitor, was done using the `request-country` package of npm.


## Problem
Listing all countries and their data

## Solution
1. Used a [json file](https://github.com/samayo/country-json/blob/master/src/country-by-name.json) for getting all country names and their code.


## Problem
Getting state specific data for only India

## Solution
1. State specific data wasn't there while I was working

2. Used [cheerio](https://cheerio.js.org/), got the website information from state website and scraped information from it
Here is an example:
```
let $ = cheerio.load(state);
  let allText = $('body').text();
  let dataArr = allText.replace(/\s\s+/g, '\n').split('\n').filter(val => (val != ''));
  let stateData = {}
  if (dataArr.length > 0 && parseInt(dataArr[0])) {
    stateData['attributes'] = {}
    stateData['attributes']['State_Region'] = dataArr[1];
    stateData['attributes']['Confirmed'] = parseInt(dataArr[2]);
    stateData['attributes']['Recovered'] = parseInt(dataArr[3]);
    stateData['attributes']['Death'] = parseInt(dataArr[4]);
    return stateData;
  }

  return null;
```

