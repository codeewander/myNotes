---
tags:
  - "#JavaScript"
  - "#DOM"
  - "#Event"
---
### Event 事件

#### 概念
- The event interface represents an event which takes place in the DOM.
- An event can be triggered by the user action.   
- 例如：使用者點擊按鈕，會跳出對話窗，則「點擊按鈕」為事件(event)，跳出對話窗為事件處理器(event handler) 

#### 常見事件
- Mouse events 滑鼠事件
	- `click` - 點擊元素
	- `mouseover/mouseout`: 當滑鼠滑動到元素上方/離開元素
	- `mousedown/mouseup`: 當滑鼠在元素上點擊/放開
- Keyboard events
		- `keydown/keyup`: 鍵盤按壓/放開
- Form element events 
	- `focus`: 當使用者正在操作某元素例如：`<input>`
	- `submit`: 當使用者送出 `<form>`
#### 事件處理器 Event handlers 
當事件觸發之後執行的函式，有三種綁定DOM的方式：

##### 1. HTML 標籤直接寫JS 
```html
<input onclick="alert('hi')" type="button" value="click me"/>
```
此做法一個事件只能綁定一個函式，且容易被駭客植入惡意程式碼，較不推薦

##### 2. on-event 處理器
在元素上直接綁定on-event ，例如 `elem.onclick`
```html
<input id ="elem" type="button" value="click me"/>
<script>
	elem.onclick = function (){
		alert('hi')
	}
</script>
```

此做法一個事件只能綁定一個函式
##### 3. 事件監聽 addEventListener

可以在一個事件上綁定多個事件處理器

```js
element.addEventListener(event, handler,[options])

// 第三個參數options 設定是否在冒泡階段(bubbling)觸發，為boolean值，預設為 false
// 若為 true，則是在事件捕捉(capturing)階段觸發 
```
[[Event capturing and bubbling]]

```html 
<input id="elem" type="button" value="click me"/>
<script>
	function handler1(){
		alert('h1')
	}
	function handler2(){
		alert ('thank')	
	}
	elem.addEventListener('click', handler1)
	elem.addEventListener('click', handler2)
</script>

```




