# Brief

Stanza is a webapp (stanza.co) which aggregates sports calendars for users. Users would subscribe to teams and the team calendars get synced to google calendar with stanza and also there would be additional information like tickets for the match etc., We were working on the dashboard part of stanza, a dashboard for managing their scrapers.  I made that part of stanza from scratch, they only had designs and rough ideas on what the essential things would be, with one to one communications with clients over weeks we made the scraper dashboard with react ,redux and express server on the backend(node). 

Stack: React.js

## Problem
Socket client for notifying when the scrapers completed their tasks


## Solution
1. Apart from the basic dashboard stuff of getting scrapers from the backend, there was a requirement to automate and notify from the dashboard when the scrapers have completed. Built the dashboard by myself

2. Wrote the client side part of sockets for push notifications
Example:
```
function displayNotification() {
  if (Notification.permission == 'granted') {
    navigator.serviceWorker.getRegistration().then(function(reg) {
      reg.showNotification('Hello world!');
    });
  }
}
```
