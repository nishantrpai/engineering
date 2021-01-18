# Brief

Cloud dashboard was the placeholder name for the project. We were working on this project to integrate all clouds on one dashboard for cloud admins. The clients we were building for internally had many users who used to interact with multiple cloud interfaces to provide services, which wasn’t scalable. They wanted to build a dashboard and all APIs underneath would communicate with all cloud providers. This would save them time in training and scaling the operations. I was responsible for building the project from scratch, built it using Next.js (Client side) + Node.js (server side) + Mongodb (DB for storing the preferences from each cloud provider as backup).

## Problem
Combine multiple cloud APIs under one dashboard, integrating multiple clouds was difficult because every API had their own implementation of response (no standard declaration).

## Solution
1. Used cloudflare API response as THE standard and every other clouds response was mapped for that, if there were values absent they were substituted with null values.

2. Key mapping was customized so any dev on the team could edit it.

## Problem
Caching the settings if cloud services are down

## Solution
Wasn't a frequent occurence but to avoid the APIs failing in the event that cloudflare APIs were down we maintained a copy in the backend which would update on the next request.