---
title: SSG vs SSR
nav_order: 4
parent: Articles
---

# SSG vs SSR

Frameworks like Next.js or Astro allow:
- **SSG(Static Site Generation)** -> looks dynamic at built time but is actually static
- **SSR(Server Side Rendering)** -> runs backend on every request

> With SSG, you can build dynamic-looking websites that can be hosted on static platforms like Github Pages or Vercel.

### Dynamic Behaviour can be simulated by:
- Fetching data from public API's using *JS in the browser*
- Building the site using SSG tools like Next.js/Eleventy and deploying the prebuilt version.