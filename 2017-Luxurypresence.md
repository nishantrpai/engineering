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

## Problem

Taking the JSON data as input, render components.
Parser from JSON -> Components -> HTML

For e.g.,
```
{{
    component: 'Header'
    props: {
        'Heading': 'Value',
        'Subheading': 'Sub-heading'
    }
    children: [
        {
            component: ''

        }
    ]
    }
}
```

## Solution
1. Common folder structure was required.

2. When the webpack builds the website, you have to deserialize

3. We had an internal mapping of keys and components, to import. The problem with this approach was all elements were renderred regardless of whether we were using them or not (wasn't resolved). A better approach would have been dynamic imports or lazy imports, although we were on the point of no return, the codebase was responsible for around 10-20 popular real estate websites, so making any changes would mean bugs in all of them. We kept that in the backlog.


4. If you want to understand this problem better, this [blog](https://www.storyblok.com/tp/react-dynamic-component-from-json) does a good job explaining how to accomplish this.
5. Also to resolve, children we used graph DFS approach:
```
  const renderComponent = (block) => {
      <Component[block.component] {block.props} > -> {renderComponent(block.children)} -> </Component[block.component]>
   }
```

## Problem
Mapping json for domain name

## Solution
1. For each website there was a domain associated with it for e.g.,
```
{
    'website_title': 'Title',
    'website_domain': domain.com
}
```