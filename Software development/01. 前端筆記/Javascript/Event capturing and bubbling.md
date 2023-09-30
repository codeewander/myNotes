---
tags:
  - "#Event"
  - "#EventDelegation"
  - "#DOM"
  - "#Capture"
  - "#Bubble"
---


### 捕獲事件和冒泡事件

DOM 事件傳遞機制分成 3 階段：

```
1：Capturing Phase　捕獲階段
2：Target Phase     傳遞到元素本身
3：Bubbling Phase   冒泡階段
```

當事件觸發時，會先進入捕獲階段(Capturing)，到達事件目標(Target)，而後才會進入冒泡階段(Bubbling)

#### 捕獲階段(Event capturing)
假設Event Target 為 `li` ，在捕獲階段事件處理器的觸發順序為：
`li` => `ul` => `div` => `body` => `document`

#### 冒泡階段(Event bubbling) 
假設Event Target 為 `li` ，在冒泡階段事件處理器的觸發順序為：
`li` => `ul` => `div` => `body` => `document`

#### DOM Event Flow

![[DOM Event Flow.png]]

#### ### 阻止事件傳遞 `e.stopPropagation`

當使用 `event.stopPropagation()`，事件傳遞就會停在設置的地方：

- 若在捕獲階段：阻止事件往下傳遞
- 若在冒泡階段：阻止事件向上傳遞

`event.stopPropagation()`這樣就可以阻止事件繼續傳遞

例如，在 window（最上層）的捕獲階段設置 event.stopPropagation，會阻止後續事件傳遞，造成所有 click 事件均失效

```js
// 監聽 window 捕獲階段的 click 事件，執行函式內指令
window.addEventListener('click', function(e) {
  e.stopPropagation()
}, true)
```


#### 阻擋預設行為 `e.perventDefault`

常見使用情境為阻止超連結的預設行為(新開分頁或跳轉)

```js
link.addEventListener("click", function (e) {  
  e.preventDefault();
});
```


[DOM 的事件傳遞機制：捕獲與冒泡](https://blog.techbridge.cc/2017/07/15/javascript-event-propagation/)
[Bubbling and capturing@JS Info](https://javascript.info/bubbling-and-capturing)

#### `e.target` v.s `e.currentTarget`

- e.target - 實際觸發事件的元素
- e.currentTarget - 事件綁定的元素（被監聽的元素）

```html
// 範例：將事件綁定在 ul 上
<head>
<script>
	let ul = document.querySelector('ul')
	ul.addEventListener('click', e=>{
		e.target.style.color = 'blue'
		e.currentTarget.style.color = 'red'	
	})
</script>
</head>
<body>
	<ul>
		list
		<li>About</li>
		<li>Project</li>
	</ul>
</body>
```

當點擊`ul`時，`e.target` 和 `e.currentTarget` 皆為 `ul`，當點擊`li`時，`e.target`為 `li` ，但`e.currentTarget` 為 `ul` 


