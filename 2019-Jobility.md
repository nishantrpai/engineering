# Brief

Jobility is building a platform for connecting daily wage workers with companies who are looking for a day or two of work. They have two web apps, one is for the workers and one is for the companies. One is an admin dashboard with which they can monitor all the workers, the companies, the ongoing work and so on and so forth. I was working on the dashboard part and was the only dev responsible for building the entire webapp from scratch.

Stack: React.js

## Problem
Same components multiple codebases

## Solution
- There was an admin dashboard, a worker dashboard and a company dashboard

- Although projects were separated by folders, the problem was maintaining components across projects

- We updated the components manually, but we wanted to move into resolving the problem once and for all which was having a common component library across projects.

- The solution to this problem wasn't separating the component library from every project. It was to combine all projects under 1 and update only the subdomains.

- One of the reasons why so many different projects happened because of different subdomains. All had to be hosted on different subdomains so everyone had to be made into a different project.

- This is a good [discussion](https://stackoverflow.com/questions/61884567/subdomain-routing-in-react-and-react-router) for this topic, but since we never implemented that solution it remained an unsolved problem.