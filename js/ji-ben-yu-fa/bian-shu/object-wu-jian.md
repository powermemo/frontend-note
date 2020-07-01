---
description: 類似arrays
---

# 物件屬性\(object properties\)

## 建立變數的物件屬性\(object properties\)

在宣告的變數後加入「={}」，  
再大括號「{}」內加入變數的物件屬性。  
屬性的值，打在冒號「:」後面。  
一個屬性以上，用逗號區隔「,」。

用一隻貓來舉例

```javascript
var cat = {
  "name": "Whiskers",
  "legs": 4,
  "tails": 1,
  "enemies": ["Water", "Dogs"]
};
```

### 從外部新增屬性

```javascript
var ourDog = {
  "name": "Camper",
  "legs": 4,
  "tails": 1,
  "friends": ["everything!"]
};

ourDog.bark = "bow-wow";//這是新增的部分
```

## 使用物件屬性

* 在變數後方加上點「.」，後方加上物件的屬性。
* 在變數後方加上中括號「\[\]」，裡面加上物件的屬性（例如有空白時可以這樣用）。
* 也可以用其他方法去定義屬性 「var 「自定義」 =  某變數的屬性」

範例：

{% tabs %}
{% tab title=".點點" %}
```javascript
var myObj = {
  prop1: "val1",
  prop2: "val2"
};
var prop1val = myObj.prop1; // val1
var prop2val = myObj.prop2; // val2
```
{% endtab %}

{% tab title="\[\]中括號" %}
```javascript
var myObj = {
  "Space Name": "Kirk",
  "More Space": "Spock",
  "NoSpace": "USS Enterprise"
};
myObj["Space Name"]; // Kirk
myObj['More Space']; // Spock
myObj["NoSpace"];    // USS Enterprise
```
{% endtab %}

{% tab title="定義屬性" %}
```javascript
var dogs = {
  Fido: "Mutt",  Hunter: "Doberman",  Snoopie: "Beagle"
};
var myDog = "Hunter";
var myBreed = dogs[myDog];
console.log(myBreed); // "Doberman"

//myBreed == dog[myDog] == dog[Hunter: 'Doberman']
```
{% endtab %}
{% endtabs %}

## 更改屬性

{% tabs %}
{% tab title="原" %}
```javascript
var ourDog = {
  "name": "Camper",
  "legs": 4,
  "tails": 1,
  "friends": ["everything!"]
};
```
{% endtab %}

{% tab title="hot更改" %}
```javascript
ourDog.name = "Happy Camper"; //這是一種方法
ourDog["name"] = "Happy Camper"; //這是另一種方法
```
{% endtab %}
{% endtabs %}

## 刪除屬性

```javascript
var ourDog = {
  "name": "Camper",
  "legs": 4,
  "tails": 1,
  "friends": ["everything!"],
  "bark": "bow-wow"
};

delete ourDog.bark;//這行進行屬性刪除
```

## 查詢屬性

利用「switch」的語法lookup

```javascript
var alpha = {
  1:"Z",
  2:"Y",
  3:"X",
  4:"W",
  ...
  24:"C",
  25:"B",
  26:"A"
};
alpha[2]; // "Y"
alpha[24]; // "C"

var value = 2;
alpha[value]; // "Y"
```

## 測試是否有該屬性

* 單筆查詢：「hasOwnProperty」
* 條列全部：「`for` \( `var` 自定義變數名 `in` 查詢的變數名稱\){}」

```javascript
function checkObj(obj, checkProp) {
  if(obj.hasOwnProperty(checkProp)) {
    return obj[checkProp];
  } else {
    return "Not Found";
  }
}
```

老師教的另一個\(vue會用到的\)

```javascript
for ( var key in myObj){
    console.log(myObj[key]);
}
/*key是自定義的
 ​*console.log會列出所有的屬性及其值。*/
```

## 判斷屬性型態

```javascript
if (typeof myObj.age === 'number'){
    console.log('YES');
}else{
    console.log('NO');
}
//判斷「myObj.age」是不是一個數值。
```

## ES6語法

### 語法糖\(syntactic sugar\)

```javascript
//以下是原本的樣子
const getMousePosition = (x, y) => ({
  x: x,
  y: y
});

//以下是語法糖簡化的樣子
const getMousePosition = (x, y) => ({ x, y });
```



