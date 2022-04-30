# String字串

##

用引號框住，單引號雙引號皆可，不要亂用就好（頭尾要一樣）。\
例如：

* `var str = 'Hello';` :white\_check\_mark:&#x20;
* `var str = "Hello";` :white\_check\_mark:&#x20;
* `var str = "Hello';` :x:&#x20;

如果字串想要有符號在內，例如「`var str = "我說"我真帥啊！""`」 :x: 是無法定義為字串的。\
要透過「\」，將「\」右方的符號轉為文字(跳脫字元)。\
例子調整為&#x20;

```javascript
var str = "我說\"我真帥啊！\""; 
console.log('str');//其結果為「我說"我真帥啊！"」
```

其他應用：

* \n，表示換行
* \t，表示tab鍵的空白
* \b，表示space鍵的空白
* \\\，表示\\
* \r，carriage return「回車」。\
  在某些作業系統中會換行，某些(例如微軟)則不行。
* \f，換頁

## 強制轉換為String

{% tabs %}
{% tab title=".toString();" %}
#### 方法一－$$x$$**`.toString();`**  //這是一個方法(v.)

範例：

`var a = 123;`\
`var b = a.toString();`//a是數值，b是字串。

`var a = 123;`\
`a = a.toString();` //a是字串。

{% hint style="info" %}
null 與 undefined沒有toString的方法（無法轉換為字串）。 :x:&#x20;
{% endhint %}
{% endtab %}

{% tab title="String();" %}
#### 方法二－`String(`$$x$$`);` //這是一個函數

範例：

`var a = 123;`\
`a = String(a);`//a是字串

{% hint style="info" %}
null 與 undefined可以透過String();轉換為字串。 :white\_check\_mark:&#x20;
{% endhint %}
{% endtab %}
{% endtabs %}

## 字串處理

### 字串長度

&#x20;`String`通過`.length`找到值的長度。\
舉例：`"Alan Peter".length;` // 10

### 字串調用的**方法**

```javascript
var s = "Hello, world"; //先創建一些文字。
s.charAt(0);             //第一個字元「h」（JS從0開始算）
s.charAt(s.length-1);    //最後一個字元「d」
s.substring(1,4);        //從第二個字(1)開始，到第四個字(4(-1))「ell」
s.slice(1,4)            //結果同上
s.slice(-3)            //倒數三個字元「rld」
s.indexOf("l");        //字母l的位置「2」
s.lastIndexOf("l");    //最後一個字母l的位置「10」
s.indexOf("l",3)        //位置3(包含3)後第一個"l"位置「3」
s.split(", ")            //切為陣列，["Hello", "world"]
s.replace("H", "h")    //用"h"取代所有"H"。「hello, world」
s.toUpperCase()        //轉為大寫「HELLO, WORLD」
```

找出第一個字 字串 `var myFirstStr = myFirstStr[0];`\
找出最後一個字 `var myFirstStr = myFirstStr[myFirstStr.length-1];`\


## ES6語法

### 模板文字Template Literals(反引號與佔位符號)

像是word的「[合併列印](https://www.managertoday.com.tw/articles/view/52854)」的「插入合併欄位」ex. 貴子弟 <姓名>\
是PHP的「[表單欄位取得變數](https://memoru86.gitbook.io/front-end-note/php/ji-ben-zhi-hang-yu-jian-jie#biao-chan-lan-wei-bian-shu-qu-de)」，ex.`echo '使用者：'$_GET['memId']`

```javascript
const person = {
  name: "Zodiac Hasbro",
  age: 56
};

// 🔸Template literal with multi-line and string interpolation
const greeting = `Hello, my name is ${person.name}!
I am ${person.age} years old.`;

console.log(greeting); // prints
// Hello, my name is Zodiac Hasbro!
// I am 56 years old.
```

{% hint style="info" %}
* **backticks**反引號 (`` ` ``)，你可以不用寫一堆加號(+)串聯字串，直接enter不用打換行符號(\n)
* **placeholder**佔位符號`${variable}` ，直接代表某個定義的JS字符。
{% endhint %}





##

##
