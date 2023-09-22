---
aliases: 
date: 2023.09.23
mindmap-plugin: basic
---

### **Importance of Rendering Patterns**

![[Rendering performance.png]]
#### Better user experience(UX) 
- [[Web Vitals]]

#### Better developer experience(DX)
- **Faster builds times 快速建構** : build fast for quick iteration and deployment  
- **Low server costs 低伺服器成本** : limit and optimize the server execution time to reduce execution costs
- **Dynamic content 動態內容** : be able to load dynamic content performantly 
- **Easy rollbacks 快速還原**: deployment can easily be reverted to a pervious version 
- **Reliable uptime 可被及時訪問: users should always be able to visit the website through operational servers
- **Scalable infrastructure可擴充架構**: easily grow or shrink without running into performance issues

### 常見模式：
- [SSG (Static Site Generation/ Static Rendering) 靜態渲染](#SSG)
- SSR (Server-Side Rendering) 伺服器端渲染- rendering a client-side or universal app to HTML on the server.
- CSR (Client-Side Rendering) 客戶端渲染 - rendering an app in a browser, generally using the DOM.


#### SSG 
👍
- HTML gets generated at build 
- Easily cacheable by CDN or an edge network 
👎
- dynamic content, customized data  

1. Plain Static Rendering 
   🚀 Use case
	   - pages that don't require request-based data 
	   - ![[Plain static rendering.png]]

2. **Static with client-side fetch** 靜態渲染加上客戶端獲取資料: dynamic data gets fetched client-side 
   🚀 Use case: 
	   1. pages that contain data that should refresh on every page load 
	   2. pages that contain stable placeholder components 
	 ![[Static with client-side fetch.png]]

3. Incremental static regeneration 增量靜態生產
		- generate some pages at build time, others on-demand 
		- automatically invalidate cache/regenerate pages
		- reduce build times 
		- easily cacheable by CDN
	🚀 Use case: 
		- Pages that should be generated on a certain interval or on-demand
		- are not user-specific 
		- can be cached globally 

#### SSR
- The generated HTML content is unique to every request and should not be cached by the CDN.
👍
-  dynamic content, customized data 
- SEO
👎
- HTML page is generated on every request 
- Poor user interaction
🚀 Use case
	- Pages contain highly personalized content
	- use request-based data, such as cookies
	- should be render-blocking
####  CSR
- Rendering pages directly in the browser with JavaScript. All logic, data fetching, templating and routing are handled on the client rather than the server.
👍
- Fast Initial Load: the server sends minimal HTML and the client loads most of the content and assets asynchronously.
- Rich User Interactions
👎
- SEO challenges
- Initial load time : have to wait for JavaScript to load and execute before they see the content
- Performance for Low-End Devices 
🚀 Use case
	- SPA (single page application)

### Reference 
- [了解網頁的三大渲染模式](https://www.webdong.dev/post/rendering-pattern/)
- [Rendering pattern - Introduction](https://www.patterns.dev/posts/rendering-patterns)

