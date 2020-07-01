---
description: 可以理解成是字串的一種嗎@@?
---

# Array陣列

可以將多個值分配在同一個變數中。  
例如：  
 `var sandwich = ["peanut butter", "jelly", "bread"]`。

巢狀陣列  
例如：  
`var arr = [  
  [1,2,3],  
  [4,5,6],  
  [7,8,9],  
  [[10,11,12], 13, 14]  
];  
  
arr[3]; // equals [[10,11,12], 13, 14]  
arr[3][0]; // equals [10,11,12]  
arr[3][0][1]; // equals 11`

## 修改陣列內資料\[\]

直接指定陣列變數的第幾的字，再給他分配值。  
例如：  
`var ourArray = [50,40,30];  
ourArray[0] = 15; // equals [15,40,30]`

## 屬性

```javascript
delete foods.apples;//🔹delete🔹刪除「foods」中的「apples」屬性。
users.hasOwnProperty('Alan');//🔹hasOwnProperty🔹檢查「users」有沒有「'Alan'」這個屬性
'Alan' in users;//🔹in🔹檢查「users」有沒有「'Alan'」這個屬性
```

## 方法

```javascript
//快速統整XD
str.split(" ",3);//用「空白鍵切割，給頭3個項目」
array.splice(2, 2);//從第三個項目[2]開始刪除兩個項目
weatherConditions.slice(1, 3);//🔸參數(從第2項目開始, 從第4【前】結束)
let thatArray = [...thisArray];//🔸ES6語法複製的方法
fruits.indexOf('oranges'); // returns 2(若是-1是沒找到的意思)
```

{% tabs %}
{% tab title="split\(\)切割" %}
```javascript
var str="How are you ?"
var splits1 = str.split(" ");
var splits2 = str.split("");
var splits3 = str.split(" ",3);
//🔸參數(用甚麼切割[，切割成幾個陣列項目])
//splits1 contains ["How", "are", "you", "?"]
//splits2 contains ["H", "o", "w", " ", "a", "r", "e", " ", "y", "o", "u", " ", "?"]
//splits3 contains ["How", "are", "you"]
```
{% endtab %}

{% tab title="splice\(\)刪除\|新增" %}
```javascript
//🔸刪除
let array = ['today', 'was', 'not', 'so', 'great'];
array.splice(2, 2);
// 從第三個項目[2]開始刪除兩個項目
// array ['today', 'was', 'great']

//🔸新增
const numbers = [10, 11, 12, 12, 15];
const startIndex = 3;
const amountToDelete = 1;
numbers.splice(startIndex, amountToDelete, 13, 14);//(3,1,13,14)
// 陣列第四個項目開始刪除一個項目，並新增「13,14」兩個項目進去。
console.log(numbers);
// returns [ 10, 11, 12, 13, 14, 15 ]
```
{% endtab %}

{% tab title="slice\(\)複製" %}
```javascript
let weatherConditions = ['rain', 'snow', 'sleet', 'hail', 'clear'];
let todaysWeather = weatherConditions.slice(1, 3);
//🔸參數(從第幾個項目開始, 從第幾個項目【前】結束)
// todaysWeather 等於 ['snow', 'sleet'];
// weatherConditions 沒有變 ['rain', 'snow', 'sleet', 'hail', 'clear']
```
{% endtab %}

{% tab title="ES6複製" %}
```javascript
//🔸ES6語法複製的方法「變數名= [...陣列變數名]」
let thisArray = [true, true, undefined, false, null];
let thatArray = [...thisArray];
// thatArray 等於[true, true, undefined, false, null]
// thisArray 沒有變, 跟thatArray的陣列項目相同
```
{% endtab %}

{% tab title="indexOf\(\)尋找" %}
```javascript
let fruits = ['apples', 'pears', 'oranges', 'peaches', 'pears'];
fruits.indexOf('dates'); // returns -1，沒有找到為-1
fruits.indexOf('oranges'); // returns 2
```
{% endtab %}
{% endtabs %}

## .push\(\)將資料加到陣列尾端

在陣列變數後加入「.push\(新增尾端陣列資料\)」的方法。

{% tabs %}
{% tab title="舉例一" %}
```javascript
var arr1 = [1,2,3];
arr1.push(4);
// arr1 is now [1,2,3,4]
```
{% endtab %}

{% tab title="舉例二" %}
```javascript
var arr2 = ["Stimpson", "J", "cat"];
arr2.push(["happy", "joy"]);
// arr2 now equals ["Stimpson", "J", "cat", ["happy", "joy"]]
```
{% endtab %}
{% endtabs %}

## .pop\(\)將陣列尾端資料刪除

舉例：  
`var threeArr = [1, 4, 6];  
var oneDown = threeArr.pop();  
console.log(oneDown); // Returns 6  
console.log(threeArr); // Returns [1, 4]`

## .shift\(\)將陣列頭端資料刪除

`var i= ["Stimpson", "J", ["cat"]];  
var u = i.shift();  
// u 現在等於 "Stimpson" i 現在等於["J", ["cat"]].`

## .unshift\(\)將資料加入陣列頭端

與「.push\(\)」的作用方式完全相同，只是「.unshift\(\)」是在頭端新增。  
舉例\(刪除後新增\)：  
`var i = ["Stimpson", "J", "cat"];`  
`i.shift();` //\(移除第一筆資料\) i 現在等於\["J", "cat"\]  
`i.unshift("Happy");`  //新增第一筆資料 i 現在等於now equals \["Happy", "J", "cat"\]  


