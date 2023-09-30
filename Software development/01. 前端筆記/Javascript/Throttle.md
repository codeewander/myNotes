---
tags:
  - "#Throttle"
  - "#DOM"
  - "#Performance"
  - "#JavaScript"
---

### Throttle 節流

![[throttle.png]]

#### 概念
- Call a function after T the first click is executed immediately. 從第一次觸發開始，在 T 秒後執行函式，中間無論觸發多少次都不會執行
- 一段時間內只會觸發一次

#### 適用情境
監聽滾動事件

#### 
```js
function throttle(fn, delay=500) {
  let timer = null; 

  return (...args) => {
	// 如果有計時器，表示還在delay秒數內，則直接 return 跳出
    if(timer) return 
  
    // 設定計時器，在 delay 秒數之後，執行fn，並將計時器清空
    // 如果還不到 delay 秒數，則 timer 值不為null，不會進到這段邏輯
    timer = setTimeout(() => { 
        fn(...args);  
        timer = null; 
    }, delay);

  };
}

const updateThrottleText = throttle(()=>{
	console.log('throttle')
}, 500)

// 監聽滾動畫面，每500 ms會印出 throttle 文字
window.addEventListener('scroll', ()=>{
	updateThrottleText()
})
```



>[!info]
> [[debounce]] 和 throttle 都是用於優化效能，但概念和使用場境不同
> 

>[!info]
> 監聽滾動事件不適合用 debounce 處理，是因為 debounce 只會在事件停止被觸發後的一段時間內執行一次，如果用 debounce ，則如果使用者一直滾動頁面永遠不會觸發函式，只會在停止滾動時執行

- [# Throttling in JavaScript Easiest Explanation](https://dev.to/jeetvora331/throttling-in-javascript-easiest-explanation-1081)