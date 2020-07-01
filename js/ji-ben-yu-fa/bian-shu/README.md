---
description: var | let | const
---

# 變數

## 宣告變數

`var` 變數名稱`;`

### 分配值給變數

\(Storing Values with the Assignment Operator\)  
`var a;   
var b = 2;`

## let

let 變數與var相似，它更傾向於「**區域變數**」。  
在哪個敘述句定義，它就是那個敘述句的變數，不會被定義為全域變數。

##  const

const變數，它的變更條件受限，你不能隨意或是無法變動它定義的值。

```javascript
const X = 'John';
const X = 'Allen'; //❌ error!!
```

通常命名的時候，全部使用大寫還有底線，例如  
`const` **`FAV_COLOR`** `= 'red';`

```javascript
'use strict';//嚴格
const s = [5, 6, 7];
s = [1, 2, 3]; // ❌錯誤，不會被執行
s[2] = 45; // ✔ ​可以被執行，陣列內的第3個值已被變更。
console.log(s); // returns [5, 6, 45]
```

## Object.freeze  不要變動 變數的值

看到上面const定義的陣列，「欸幹，我都用const你還給我變動裡面的值?!」  
這時候就使用**`Object.freeze()`**，你變數定義的值就無法變更囉～

```javascript
let obj = {
  name:"FreeCodeCamp",
  review:"Awesome"
};
Object.freeze(obj);//🔸
obj.review = "bad"; // 被忽略，變更不被允許
obj.newProp = "Test"; // 被忽略，變更不被允許
console.log(obj); // { name: "FreeCodeCamp", review:"Awesome"}
```

