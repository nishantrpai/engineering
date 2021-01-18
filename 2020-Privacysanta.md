# Brief

Privacysanta is a webapp to generate a privacy policy for your website.Generate privacy policy compliant with GDPR/CCPA. Internally, privacy santa has multiple rules which are based on GDPR, and was a turnkey SaaS tool to generate based on user inputs while making sure it was compliant with GDPR. The struggle was in going through GDPR rules and turning them into actual forms and rendering conditionally. The project was built from scratch by me using Next.js and Firebase.

Stack: Next.js + Firebase


## Problem
Rendering from JSON to interface of UI + Text

## Solution
1. Core of the product was storing privacy policies in JSON and rendering them into two interfaces

2. Was making requests to the backend with the subdomain from the URL, since privacy policies were stored internally based on their domain it made making requests to the backend much easier.

3. The key problem was rendering them the server side, not the client side. If you retrieve data from the client side
a. The API would get exposed
b. Would be a poor first experience of the app

4. Next.js had an internal implementation to take care of this 
```
function Page({ stars }) {
  return <div>Next stars: {stars}</div>
}

Page.getInitialProps = async (ctx) => {
  const res = await fetch('https://api.github.com/repos/vercel/next.js')
  const json = await res.json()
  return { stars: json.stargazers_count }
}

export default Page
```

## Problem 
Autocomplete on search

## Solution

1. While selecting tools in the privacy policy, there was a need for getting tools based on user input.

2. Although, I don't like this implementation. It was pre-fetching all tools that the app uses and based on user input the most likely tool was selected.

```
    let possibleTools = tools.filter(tool => tool.includes(userInput));
```

## Problem
Maintaining state across the entire app

## Solution
1. The current system we had used state from the main app and that was passed across all children, but this was in hindsight a poor implementation.

2. A better implementation would have been using [context provider](https://reactjs.org/docs/context.html#when-to-use-context), which does this.

```
// Context lets us pass a value deep into the component tree
// without explicitly threading it through every component.
// Create a context for the current theme (with "light" as the default).
const ThemeContext = React.createContext('light');

class App extends React.Component {
  render() {
    // Use a Provider to pass the current theme to the tree below.
    // Any component can read it, no matter how deep it is.
    // In this example, we're passing "dark" as the current value.
    return (
      <ThemeContext.Provider value="dark">
        <Toolbar />
      </ThemeContext.Provider>
    );
  }
}

// A component in the middle doesn't have to
// pass the theme down explicitly anymore.
function Toolbar() {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}

class ThemedButton extends React.Component {
  // Assign a contextType to read the current theme context.
  // React will find the closest theme Provider above and use its value.
  // In this example, the current theme is "dark".
  static contextType = ThemeContext;
  render() {
    return <Button theme={this.context} />;
  }
}
```