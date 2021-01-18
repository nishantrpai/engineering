# Brief

Ninjavan is working on making a CMS system for e-commerce websites with reactjs. Currently they made a website with their existing component library in react, an ecommerce website called kjustore.com and wanted to replicate their logic of rendering using api in other ecommerce websites as well, so we were designing components to handle such logic for them in reactjs.

Stack: React.js 

## Problem
Bug: Multiple checkouts on the day of launch

## Solution
1. Apart from all the implementation problems and testing issues, this was perhaps the most terrifying problem I faced and it happened on the worst possible day.

2. The problem was during dev, the checkout worked fine. But, on the day of launch there was a serious bug of checking out once, but transactions happening multiple times compound that with a big launch day.

3. The technical problem was using redux thunk. The accurate problem we solved is still difficult to recollect, but the main problem was combining reducers with same name caused that issue.

How redux works:
```
getdata(api) -> dispatch(updateInfo(data))
```

How redux thunk works:

Since you can't dispatch 

```
dispatch(updateInfo()) 

updateInfo() {
    getdata(api).then(data => dispatch({type: 'UPDATE_INFO', data }))
}
```

You can make it do some actual actions like getting data from api and dispatching it internally on the store.

The problem was the next action was triggered with a similar key.

After hours of debugging, finally fixed it.

4. Reasons why this happened:

a. Large codebase: It was responsible for making sure you could generate an ecommerce site.

b. Poor documentation: When you can't read prior code, adding new code gets very dangerous. That part was on me, if I read the code correctly and understood the underlying architecture this incident could have been avoided. For future events, that would be my approach to dealing with large codebases, spend time documenting before adding any new code. 

c. Lack of testing: Since the other team I was working with was extremely busy testing was discounted. Even I made the assumption that someone on their end would manually test before deploying, but that didn't happen and on the day of launch we had to face those issues.