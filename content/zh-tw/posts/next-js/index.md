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

淺談Next.js
==

1. 甚麼是Next.js?
>React 的Framework
>
**功能:** 在Server 時就rander 你的app 
**舉例:**
>像是傳統React、Angular、Vue這種SPA(single page application)的特性是在切換不同網頁時，是直接用javascript更改畫面讓讀取速度比一般網頁快一些，而不是去Server下載整個頁面。

缺點：有時要在客戶端抓取資料，也就是說使用者打開網頁時，SPA才會使用js去server抓資料，如果google要爬你的網頁時，就無法爬到你的內容，因為網頁是要等使用者打開時，才會去抓資料的動作。而Next.js就解決這個問題。
2. 兩種獲取資料的方法
* getStaticProps =你在產生網頁時，就去抓取資料然後之後每次User更新，直接傳給User已經產生好的資料，適合:久久更新的Blog
* getServerSideProps：每次User開啟都去抓資料，產生網頁給User，適合：頻繁更新的Twitter。

Next.js安裝
==
創建 Next.js 應用程式
```
npx create-next-app 
or
yarn create-next-app
```

CSR是什麼
==
CSR全稱是 Client Side Rendering ，代表的是用戶端渲染。 顧名思義，就是在渲染工作在用戶端（瀏覽器）進行，而不是在伺服器端進行。 舉個例子，我們平時用vue，react等框架開發的專案，都是先下載html文檔（不是最終的完全的html），然後下載js來執行渲染出頁面結果。

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
> 可以看出當前頁面除了 元素，沒有其他的元素，然後通過載入 ， 來執行渲染。 整個渲染過程包括，生成DOM節點，注入樣式，交互事件綁定，數據獲取等等。<div id="root"></div>bundle.jsmain.chunk.js
**優點**
1. 前後端分離。 前端專注於介面開發，後端專注於api開發，且前端有更多的選擇性，可以使用vue，react框架開發，而不需要遵循後端特定的範本。
2. 伺服器壓力變輕了，渲染工作在用戶端進行，伺服器直接返回不加工的html
3. 使用者在後續訪問操作體驗好，（首屏渲染慢）可以將網站做成SPA，可以增量渲染

**缺點**
1. 不利於SEO，因為搜尋引擎不執行JS相關操作，無法獲取渲染后的最終html。
2. 首屏渲染時間比較長，因為需要頁面執行ajax獲取數據來渲染頁面，如果請求介面多，不利於首屏渲染

SSR是什麼
==
SSR全稱是 Server Side Rendering，代表的是服務端渲染。 與用戶端渲染不同的是，SSR輸出的是一個渲染完成的html，整個渲染過程是在伺服器端進行的。 例如傳統的JSP，PHP都是服務端渲染

**優點**
1. 有利於SEO，由於頁面在伺服器生成，搜尋引擎直接抓取到最終頁面結果。
2. 有利於首屏渲染，html所需要的數據都在伺服器處理好，直接生成html，首屏渲染時間變短。

**缺點**
1. 佔用伺服器資源，渲染工作都在服務端渲染
2. 用戶體驗不好，每次跳轉到新頁面都需要在重新服務端渲染整個頁面，不能只渲染可變區域

SSG是什麼
==
SSG全稱是 Static Site Generation ，代表的是靜態網站生成。 在構建的時候直接把結果頁面輸出html到磁碟，每次訪問直接把html返回給客戶端，相當於一個靜態資源
**優點**
1. 減輕伺服器壓力，可以把生成的靜態資源（html）放到CDN上，合理利用緩存
2. 有利於SEO，由於html已經提前生成好，不需要服務端和用戶端去渲染

**缺點**
1. 只適用於靜態數據，對於經常改動的數據，需要每次重新生成頁面。
2. 用戶體驗不好，每次打開新頁面都需要重新渲染整個頁面，不能只渲染可變區域


Next.js 十大功能
==
1. Automatic Code Splitting
CODE SPLITTING可以在切換 Router的時候把需要的程式碼做分割 達到最輕量化 而加快速度，因為 Next.js 的Router的目錄是在pages底下使用 File-System 架構目錄來替代 Router 這部分的 Code Splitting 已經內建了
2. Css
Built-In Css Support
Next.js之中有內建一套 style jsx 的Css In Js 的功能，如下面的風格
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
PS. Next.js是很彈性的也可以使用其他如Jss或是 styled-component....等等的Css In Js套件
3. Static File Serving
靜態檔案的約定目錄，可以把一些靜態檔案都放在這裡例如圖檔，聲音檔案等等都可以在根目錄下的static(約定目錄),也可以透過Express去指定
4. Populating

在Next.js中因為是使用 React Render 所有的程式碼都會 Render在一個DOM節點下,如果今天要改變Document 的 Head 裡面的或是等等就可以使用 Next.js 提供的 Head 元件
```
import Head from 'next/head'
```


5. Fetching Data And ComponentT LifeCycle
Next.js提供了 Server Side Render 功能當網站使用了SSR 的部分的時候為了SPA與SSR同步 所以提供了一個生命週期 getInitialProps 方便前後端一致

```
static async getInitialProps({ req }) {
    const userAgent = req ? req.headers['user-agent'] : navigator.userAgent
    return { userAgent }
  }
```

6. Routing

>Client-Side的部分 Next.js 提供 Link 工具可以使用 import Link from 'next/link'
在轉 Routing 時候 Next.js 綁定一些功能,例如 Prefetch 功能可以提前把指定的下一頁預處理好增加ux體驗
除了Link 像使用tag A href 的方式寫在 JSX 中外 ,如果要在程式中使用 API LINK 的功能可以使用
import Router from 'next/router' 範例如下

```
export default () =>
  <div>
    Click <span onClick={() => Router.push('/about')}>here</span> to read more
  </div>
```
6. ROUTER EVENT
> 通常可以用在過場的時候,使用以下的一些EVENT管理, 常見可以用在LOADING的圖樣效果
onRouteChangeStart(url) - 開始轉換ROTUER時觸發
onRouteChangeComplete(url) - 完成時
onRouteChangeError(err, url) - 有錯誤時
onBeforeHistoryChange(url) - 如果有異動 BROWSER時

7. ShallowW Routing
再換頁的時候不去執行 getInitialProps 如果希望在同一頁底下每次的參數改變時候不執行 getInitialProps 就可以打開Shallow

8. Useing a High Order Component
React 常用的 HOC 在 Next.js 元件中也是可以使用的

9. Prefetching Pages
同上述 Router功能 ，使用 import Link from 'next/link' LINK有提供PREFETCH功能可以預先 Preload 資料的功能

10. custom Server And Routing
Next.js 可以客製化綁定常見的Server Express Koa2 Hapi Connect....等 Routing 部分也非常彈性可以完全自定義


推薦的優質資源
==

1. Next.js Document 中/英
https://nextjs.org/docs/getting-started
2. freecodecamp 英文
{{< youtube KjY94sAKLlw >}}
3. 基礎練習 適合初學者 英文
{{< youtube tsmaQdgidKg >}}