---
aliases:
---

#### Why:  **Importance of Rendering Patterns**

![[Pasted image 20230922230713.png]]
##### Better user experience(UX) 
- [[Web Vitals]]

##### Better developer experience(DX)
- **Faster builds times 快速建構** : build fast for quick iteration and deployment  
- **Low server costs 低伺服器成本** : limit and optimize the server execution time to reduce execution costs
- **Dynamic content 動態內容** : be able to load dynamic content performantly 
- **Easy rollbacks 快速還原**: deployment can easily be reverted to a pervious version 
- **Reliable uptime 可被及時訪問: users should always be able to visit the website through operational servers
- **Scalable infrastructure可擴充架構**: easily grow or shrink without running into performance issues

#### 常見模式：
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
	   - ![[Pasted image 20230923001551.png]]

2. **Static with client-side fetch** 靜態渲染加上客戶端獲取資料: dynamic data gets fetched client-side 
   🚀 Use case: 
	   1. pages that contain data that should refresh on every page load 
	   2. pages that contain stable placeholder components 
	 ![[Pasted image 20230923001520.png]]

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
👎
- HTML page is generated on every request 
- Usually slower than CSR rendering website
🚀 Use case
	- Pages contain highly personalized content
	- use request-based data, such as cookies
	- should be render-blocking
### CSR

