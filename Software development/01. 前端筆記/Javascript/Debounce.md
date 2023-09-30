---
tags:
  - "#Debounce"
  - "#DOM"
  - "#Performance"
  - "#JavaScript"
date: 2023.09.29
---
### Debounce 防抖

![[debounce.png]]

#### 概念
- Delaying the execution of a function until a certain amount of time has passed since the last time it was called  從最後一次觸發開始，在 T 秒後執行函式
- 多個連續觸發動作只執行一次
- 類似於進入電梯，當沒有人按開門按鈕之後的T秒，門才會關上(執行動作)

#### 適用情境

使用者在搜尋內打字，直到停止輸入T秒後才觸發搜尋功能，可以減少搜尋動作的觸發次數

#### 程式碼架構

接受兩個參數 1.  延遲時間(T) 2. 要執行的函式
```js
function debounce (fn, delay = 500){

	let timer = null 
	// 最終回傳一個函式
	return (...arg)=>{
		// 每次 debounce 函式被觸發時，會先清除之前的 timer，避免觸發之前的 fn函式
		// 因此只要在 delay時間內觸發 debounce函式，就會一直清除之前的 timer
		clearTimeout(timer)
		// 清除之後再重新計時
		// 當 delay 時間到時，執行 fn
		timer = setTimeout(()=>{
			fn(...args)
		}, delay)

	}
}

// updateDebounceText 函式會在延遲 500 ms後印出 debounce 文字
const updateDebounceText = debounce (text=> {
	console.log('debounce')
},500)

// 監聽 input 事件，當input改變時觸發 updateDebounceText 函式
searchInput.addEventListener('input',(e)=>{
	updateDebounceText(e.target.value)
})
```


>[!info]
> debounce 和 [[Throttle]] 都是用於優化效能，但概念和使用場境不同

>[!info] 
> 控制輸入框查詢不適合用 throttle 處理，假設使用者一開始輸入apple，馬上改成 book，用 throttle 會讓使用者輸入apple後，有t秒時間都不會執行查詢動作。


[# JavaScript Debounce, Easiest explanation !(with Code)](https://dev.to/jeetvora331/javascript-debounce-easiest-explanation--29hc)
[## 網頁 DOM 事件的效能優化：Debounce 和 Throttle](https://www.mropengate.com/2017/12/dom-debounce-throttle.html?fbclid=IwAR1ncL2Wn9giRB8tTurV_ipXpRppvP1bCv1kX5ibrZgrzw3_5s_DZ2G3St8)
