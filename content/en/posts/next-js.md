---
slug: next-js
title: what is next.js
date: 2025-10-28 12:27:20
tags:

- javascript
- next.js

categories:
  - Note

---
slug: next-js

A Brief Introduction to Next.js
==

1. What is Next.js?
>A Framework for React
>
**Function:** Renders your app on the Server
**Example:**
>Traditional React, Angular, and Vue are SPAs (Single Page Applications) that switch between pages by using JavaScript to update the view rather than downloading the entire page from the server, making navigation faster.

Drawback: Sometimes data needs to be fetched on the client side, meaning the SPA uses JS to fetch data from the server only when the user opens the page. If Google tries to crawl your page, it won't find any content because the data is fetched only when a user opens the page. Next.js solves this problem.

2. Two methods for fetching data
* getStaticProps = Fetches data when the page is generated; thereafter, every time a user refreshes, the pre-generated data is served directly. Suitable for: blogs that update infrequently.
* getServerSideProps: Fetches data and generates the page every time a user opens it. Suitable for: frequently updated platforms like Twitter.

Next.js Installation
==
Create a Next.js application
```
npx create-next-app 
or
yarn create-next-app
```

What is CSR
==
CSR stands for Client Side Rendering. As the name implies, rendering is done on the client side (browser) rather than on the server. For example, projects built with Vue, React, and other frameworks first download an HTML document (not the final complete HTML) and then download JS to render the page result.

```html=
<!DOCTYPE html>
<html lang="en">
 <head> 
  <title data-react-helmet="true">react app</title> 
  <noscript> 
  </noscript>
 </head>
 <body>
  <noscript>
   You need to enable JavaScript to run this app.
  </noscript> 
  <div id="root"></div>
  <script type="text/javascript" src="/static/js/bundle.js" defer=""></script> 
  <script type="text/javascript" src="/static/js/main.chunk.js" defer=""></script> 
 </body>
</html>
```
> As you can see, the current page only has the `<div id="root"></div>` element; then `bundle.js` and `main.chunk.js` are loaded to perform rendering. The entire rendering process includes generating DOM nodes, injecting styles, binding interactive events, fetching data, and more.

**Advantages**
1. Separation of front-end and back-end. The front-end focuses on UI development, the back-end focuses on API development. The front-end also has more choices and can use Vue, React, and other frameworks without needing to follow back-end specific templates.
2. The server workload is reduced; the rendering work happens on the client side and the server returns unprocessed HTML directly.
3. User experience for subsequent visits is good (initial render is slow); the site can be built as an SPA with incremental rendering.

**Disadvantages**
1. Not SEO-friendly, because search engines do not execute JS operations and cannot obtain the final rendered HTML.
2. Initial page load time is longer because the page needs to execute AJAX requests to fetch data for rendering; if there are many API calls, the initial render is slow.

What is SSR
==
SSR stands for Server Side Rendering. Unlike client-side rendering, SSR outputs fully rendered HTML - the entire rendering process happens on the server side. Traditional JSP and PHP are both examples of server-side rendering.

**Advantages**
1. SEO-friendly, since pages are generated on the server and search engines can directly crawl the final page result.
2. Better initial render performance - the HTML has all required data already processed on the server side and is generated directly, making initial load time shorter.

**Disadvantages**
1. Higher server resource consumption, as all rendering work is done on the server.
2. Poor user experience, since every navigation to a new page requires the server to re-render the entire page rather than only the changed areas.

What is SSG
==
SSG stands for Static Site Generation. During the build process, result pages are output as HTML files to disk; every visit returns these HTML files directly to the client, essentially serving static resources.

**Advantages**
1. Reduces server load; the generated static resources (HTML) can be placed on a CDN, leveraging caching effectively.
2. SEO-friendly, since HTML is pre-generated and neither the server nor the client needs to render it.

**Disadvantages**
1. Only suitable for static data; for frequently changing data, pages need to be regenerated every time.
2. Poor user experience, since every new page requires a full page render rather than only the changed areas.


Top 10 Features of Next.js
==
1. Automatic Code Splitting
Code splitting splits the code needed when switching routes to achieve the smallest possible bundle and faster load times. Since Next.js uses a File-System based directory structure under the pages folder as its router, this code splitting is built in.

2. CSS
Built-In CSS Support
Next.js has a built-in styled-jsx CSS-in-JS solution, as shown in the example below:
```
export default () =>
  <div>
    Hello world
    <p>scoped!</p>
    <style jsx>{`
      p {
        color: blue;
      }
     </style>
   </div>
```
PS. Next.js is also very flexible and supports other CSS-in-JS libraries such as JSS or styled-components.

3. Static File Serving
A convention directory for static files. You can put static files such as images and audio files in the static directory (a convention directory) in the project root, and can also specify it via Express.

4. Populating

In Next.js, since React renders all code under a single DOM node, if you want to modify the `<head>` contents in the HTML Document (such as `<title>`, etc.), you can use the Head component provided by Next.js:
```
import Head from 'next/head'
```


5. Fetching Data And Component LifeCycle
Next.js provides Server Side Rendering. To keep the SPA and SSR in sync, it provides a lifecycle method called `getInitialProps` to maintain consistency between the front and back end:

```
static async getInitialProps({ req }) {
    const userAgent = req ? req.headers['user-agent'] : navigator.userAgent
    return { userAgent }
  }
```

6. Routing

>On the client side, Next.js provides a Link component: `import Link from 'next/link'`
When navigating routes, Next.js binds some features such as Prefetch, which pre-processes the next designated page in advance for a better UX.
In addition to using the Link component like an anchor tag `<a href>` in JSX, to use the Link functionality programmatically you can use:
`import Router from 'next/router'` Example:

```
export default () =>
  <div>
    Click <span onClick={() => Router.push('/about')}>here</span> to read more
  </div>
```
6. ROUTER EVENT
> Typically used for page transitions; manage with the following events - commonly used for loading animation effects:
onRouteChangeStart(url) - Fires when a route transition begins
onRouteChangeComplete(url) - Fires when complete
onRouteChangeError(err, url) - Fires when there is an error
onBeforeHistoryChange(url) - Fires when the browser history changes

7. Shallow Routing
Navigating between pages without triggering getInitialProps. If you want parameter changes on the same page not to trigger getInitialProps, you can enable Shallow routing.

8. Using a Higher Order Component
React's commonly used HOC pattern is also usable in Next.js components.

9. Prefetching Pages
As mentioned in the Router section above, `import Link from 'next/link'` - Link provides a Prefetch feature that can preload data in advance.

10. Custom Server and Routing
Next.js can be bound to popular servers like Express, Koa2, Hapi, Connect, etc. The routing part is also very flexible and can be fully customized.


Recommended Quality Resources
==

1. Next.js Documentation (Chinese/English)
https://nextjs.org/docs/getting-started
2. freecodecamp (English)
{{< youtube KjY94sAKLlw >}}
3. Beginner exercises - suitable for beginners (English)
{{< youtube tsmaQdgidKg >}}
