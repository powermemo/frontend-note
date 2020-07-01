# function函式

## 簡單地舉例：

```javascript
function functionName() {
  console.log("Hello World");
}
functionName(); //呼叫函式
```

function 「自定義function名稱」\(「參數\(選填\)」\){  
　函式內容;  
}

「console.log\(\);」是指，結果會印在瀏覽器裡面，你開瀏覽器按F12應該會有「開發者工具」的介面  
找到「console」的頁籤就可以看到印出的結果了。

## 加入回傳值

```javascript
function testFun(param1, param2) { //給回傳值1 以及 回傳值2
  console.log(param1 + param2); //結果會是回傳值1+回傳值2
}
testFun(4,5); //結果會是9，因為4+5😒
```

## 全域變數與區域變數

* 全域變數：
  * 使用`var`，放在「`function`」函式**外**，任何地方都可以使用→全域變數。
  * 不使用`var`，放在「`function`」函式**內**，任何地方都可以使用→全域變數。
* 區域變數：
  * 使用`var`，放在「`function`」函式**內**，僅function內部可以使用→區域變數。

```javascript
//一些例子w
var a = 10;        //a全域變數
b = 20;            //b全域變數
function f1 (x){    //x區域變數
    var c = 30;    //c區域變數
    c += 100;
    d = 40;        //d全域變數
    a += 100;
}
f1(666);
//最後的值變成----a:110、b:20、x:666、C130、d:140
```

{% hint style="info" %}
若區域變數與全域變數有相同的變數名稱，  
程式會**優先處理區域變數**。
{% endhint %}

## 使用「return」回傳值

{% tabs %}
{% tab title="使用return" %}
```javascript
function plusThree(num) {
  return num + 3;
}
var answer = plusThree(5); // 8
console.log(answer);//結果會是8
console.log(num);//結果是「undefined」
```
{% endtab %}

{% tab title="未使用return" %}
```javascript
var sum = 0;
function addSum(num) {
  sum = sum + num;
}
addSum(3); // 變數sum會被改變，但是回傳值is undefined

console.log(sum);//結果是「3」
console.log(num);//結果是「undefined」
```
{% endtab %}
{% endtabs %}

沒有使用「return」的情話下，使用函數\(及其參數\)的話，結果會是「undefined」。

## arrow function 箭頭函式

這是ES6的語法。  
好像得用「**const**」定義變數才行～

{% tabs %}
{% tab title="箭頭函式" %}
```javascript
//↓原本的function函式
const myFunc = function() {
  const myVar = "value";
  return myVar;
}


//↓改成箭頭函式
const myFunc = () => {
  const myVar = "value";
  return myVar;
}


//↓如果「沒有其他函式描述」只有回傳值的話，可以簡化成這樣
const myFunc = () => "value";
```
{% endtab %}

{% tab title="加入參數" %}
```javascript
const doubler = (item) => item * 2;
//↓如果只有一個參數，可以不用使用括號
const doubler = item => item * 2;

//↓使用 一個以上 的參數
const multiplier = (item, multi) => item * multi;
```
{% endtab %}

{% tab title="默認參數" %}
```javascript
const greeting = (name = "Anonymous") => "Hello " + name;

console.log(greeting("John")); // Hello John
console.log(greeting()); // Hello Anonymous
```
{% endtab %}

{% tab title="參數陣列" %}
```javascript
function howMany(...args) {//🔸那個「...」就是了。
  return "You have passed " + args.length + " arguments.";
}
console.log(howMany(0, 1, 2)); // You have passed 3 arguments.
console.log(howMany("string", null, [1, 2, 3], { })); 
// You have passed 4 arguments.
```
{% endtab %}

{% tab title="分配\(屬性\)" %}
```javascript
const user = { name: 'John Doe', age: 34 };


const name = user.name; // name = 'John Doe'
const age = user.age; // age = 34

//🔸↓可以改用這種寫法去取得值
const { name, age } = user;
// name = 'John Doe', age = 34
```
{% endtab %}

{% tab title="分配\(屬性\)2" %}
```javascript
const HIGH_TEMPERATURES = {
  yesterday: 75,
  today: 77,
  tomorrow: 80
};

//取得值，同時給變數名
const highToday = HIGH_TEMPERATURES.today;
const highTomorrow = HIGH_TEMPERATURES.tomorrow; 

//🔸取得值，同時給變數名  的另一種寫法
const {today: highToday, tomorrow: highTomorrow} = HIGH_TEMPERATURES;
```
{% endtab %}
{% endtabs %}

### spread 方法

{% tabs %}
{% tab title="JavaScript" %}
```javascript
//這是原本的，Math.max(arr) returns NaN.
var arr = [6, 89, 3, 45];
var maximus = Math.max.apply(null, arr); // returns 89

//↓為了更佳的可讀性，可以改寫成這樣
const arr = [6, 89, 3, 45];
const maximus = Math.max(...arr); // returns 89
```
{% endtab %}

{% tab title="錯誤訊息" %}
```javascript
//開頭沒有任何描述，使用...會回傳錯誤
const spreaded = ...arr; // will throw a syntax error
```
{% endtab %}

{% tab title="複製" %}
```javascript
//把所有值複製到另一個變數中。 using the spread operator.
const arr1 = ['JAN', 'FEB', 'MAR', 'APR', 'MAY'];
let arr2;

arr2 = [...arr1];  // 🔸

console.log(arr2);
```
{% endtab %}
{% endtabs %}

## ES6語法

簡潔的句法

```javascript
//以下是ES5的句法
const person = {
  name: "Taylor",
  sayHello: function() {
    return `Hello! My name is ${this.name}.`;
  }
};

//🔸以下是ES6的句法，你可以更簡潔地寫（省略關鍵字「function」）
//請注意，「sayHello」屬性後面的冒號「:」也被省略了。
const person = {
  name: "Taylor",
  sayHello() {
    return `Hello! My name is ${this.name}.`;
  }
};
```

### 

### 導出與共用

有一個要共用的js檔案，在這個js檔案中輸入`expert{ 函數 | 函數名 }` ，其他js檔就可以共用了～

置入使用的語法：`import { 函數名 | 變數名 } from '檔案位置';`

{% tabs %}
{% tab title="導出" %}
```javascript
//這是一個導出的方法
export const add = (x, y) => {
  return x + y;
}

//這是另一個導出的方法
const add = (x, y) => {
  return x + y;
}
export { add };
//如果你要導出多個可以這麼寫
export { add, subtract };
```
{% endtab %}

{% tab title="置入" %}
```javascript
import { add, subtract } from './math_functions.js';

//如果想要置入(導入)所有文件的資料，使用「*」以下範例
//「myMathModule 」是自定義
import * as myMathModule from "./math_functions.js";
//使用這份檔案的資料時，以下範例
myMathModule.add(2,3);
myMathModule.subtract(5,3);
```
{% endtab %}
{% endtabs %}

