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

倘若需要加載動態內容，有幾種方式：
1. **Static with client-side fetch** 靜態渲染加上客戶端獲取資料: 在靜態渲染的基礎上，在客戶端使用 JavaScript 來送出 API 請求獲得資料並更新內容
		Best for pages that: 
	- contain data that should refresh on every page load 
	- contain stable placeholder components 
3. Incremental static regeneration 增量靜態生產: 解決大量頁面導致建構時間長、動態資料無法即時呈現的問題
		- 只會事先渲染部分重要頁面，剩餘的頁面就等到有用戶請求再渲染
		- 在指定的時間由伺服器重新渲染該頁面，定期的刷新靜態頁面中的內容
		
#### SSR

### CSR
