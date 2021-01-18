# Brief

Luxury presence is a company which provides real estate agents with stunning websites. They lacked reusable components which could help building websites faster.  So we built components on react which can be reused.  Providing these individual component with their settings which can be changed from its dashboard so it’s easier to configure the component for someone who doesn’t understand coding. Page settings for example, if you want to build the ‘/about’ page it would just take 5-10 mins to build one by simply adding the components you’d need.

Stack: React.js

## Problem
Doing responsive CSS for the website

## Solution
1. The business logic was simple to implement, the real challenge in this project was CSS. There were many different designs and the web designs were supposed to be 100% accurate to the mockups.

2. The main challenge here was writing responsive css, wasn't that great at css at the start of this project, but most problems were resolved using Flexbox

```
.row {
    display: flex;
}
.column {
    display: flex;
    flex-direction: column;
}
@media only screen and (max-width: 600px) {
    /*row elements need to be rendered as columns*/
    .row {
        display: flex;
        flex-direction: column;
    }
}
```