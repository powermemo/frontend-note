---
description: ES6非同步
---

# promise

參考網站\[[link](https://www.fooish.com/javascript/ES6/Promise.html)]

## 簡介

一個 Promise 物件 (只) 會處於下面三種狀態之一：

1. pending - 初始狀態 (進行中)
2. fulfilled - 事件已完成
3. rejected - 事件已失敗

Promise 狀態的改變只有兩種可能：

1. 從 pending 變成 fulfilled
2. 從 pending 變成 rejected

{% hint style="info" %}
一但狀態改變就會固定，永遠不會再改變狀態了。

非同步最常見的例子像是 [AJAX](https://www.fooish.com/javascript/AJAX-Asynchronous-JavaScript-and-XML.html)，傳統在處理非同步事件時會用一堆 nested callbacks，Promise 則是提供另外一種解決方案，讓你更直觀地控制非同步操作。
{% endhint %}

```javascript
const makeServerRequest = new Promise((resolve, reject) => {
  let responseFromServer = false;
  if(responseFromServer) {
    resolve("We got the data");//🔸resolve
  } else {  
    reject("Data not received");//🔸reject
  }
});

makeServerRequest.then(result => {//🔸then
  console.log(result);
});

makeServerRequest.catch(error => {//🔸catch
  console.log(error);
});
```

* **resolve(value)** 函數用來將 Promise 物件的狀態變為 fulfilled (已完成)，\
  在非同步操作成功時調用，你可以將非同步操作的結果當作參數一起傳入。
* **reject(error)** 函數用來將 Promise 物件的狀態變為 rejected (已失敗)，\
  在非同步操作失敗時調用，你可以將非同步操作的錯誤當作參數一起傳入。
* **then()** 方法來綁定當 fulfilled 或 rejected 狀態(選填)時，分別要執行的函數。
* **catch()** 方法來綁定當 rejected 狀態時，要執行的函數。\
  catch() 的用途就像是 then(undefined, onRejected)。

