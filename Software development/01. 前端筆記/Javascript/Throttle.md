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
    // 倘若沒有計時器則執行fn (有計時器) 
    if (timer === null) { // If there is no timer currently running
      fn(...args);  
      timer = setTimeout(() => { // Set a timer to clear the timerFlag after the specified delay
        timerFlag = null; // Clear the timerFlag to allow the main function to be executed again
      }, delay);
    }
  };
}
```



>[!info]
> debounce 和 throttle 都是用於優化效能，但概念和使用場境不同

[[Debounce]]