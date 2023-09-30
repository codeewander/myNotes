- ES6 新功能
- 目的：優化過去使用 callback 來執行異步操作 
- 用來表示異步操作的最終完成(或失敗)以及結果值
- 是一個建構函式，同時，函式也屬於**物件**

#### 如何使用
透過 `new` 關鍵字建立 Promise ，Promise 會接受一個函式作為參數，而這個函式又稱為executor，會立即執行
```js
// console.log 會立即執行
new Promise ((resolve, reject)=>{
	console.log("executor 立即執行")
})
```

而 executor 函式會接受兩個函式參數，分別為 resolve(成功時呼叫) 和 reject(失敗時呼叫)

```js
function requestData(url) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (url === "kira.com") {
        resolve("hello welcome to kira's website");
      } else {
        reject("it is not kira's website");
      }
    }, 3000);
  });
}

// 1. 請求成功
requestData("kira.com").then((res) => {
  console.log(res); //hello welcome to kira's website
});

//2. 請求失敗
requestData("peter.com").catch((e) => console.log(e)); //it is not kira's website

```


#### Promise 的狀態

一個 Promise 一定會處於以下三種狀態的其中一種

1. pending：初始狀態，執行了 executor，但還在等待中。
2. fulfilled：表示操作完成，執行 resolve 函式。
3. rejected：表示操作失敗，執行 reject 函式。

### 錯誤處理

Promise 的一個好處是錯誤處理，最簡單的方式是在加上一個 catch 來捕捉錯誤，並執行一些錯誤處理代碼。如下方程式碼，如果請求失敗，例如由於網絡故障，則 Promise 會被拒絕。在這種情況下，catch 方法將捕獲錯誤，並輸出錯誤訊息。
`finally` 則是在不管 Promise 是否成功的狀態下，都會執行的最後操作。

```js
fetch("https://explainthis.com/data")
  .then((response) => response.json())
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.error("oops!", error);
  })
  .finally(() => {
    console.log("close loader");
  });
```

[[async await]]