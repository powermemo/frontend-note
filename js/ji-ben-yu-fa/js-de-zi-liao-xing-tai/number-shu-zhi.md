# Number數值

## 

* `var = 123;`
* MAX\_VALUE最大值，數值  `Number.MAX_VALUE;` →這是Infinity
* MIN\_VALUE大於0的最小值，數值  `Number.Min_VALUE;`
* Infinity無限，數值 
* -Infinity負無限，數值
* NaN表示「Not A Number」，數值 例如`var a = "s" * "h";` 結果就會變成「NaN」，但仍會判斷它是一個數值。

## 強制轉換為Number

{% tabs %}
{% tab title="Number\(\);" %}
### 方法一－`Number(`$$x$$`);`  //這是一個函數

#### 字串

* 如果字串是純數字，會轉為數字。 
* 如果有非數字內容，會回傳「NaN」。 
* 如果空字串或空格，會轉為數字「0」。 

範例：

`var a = "123";  
a = Number(a);` //a是一個數值，內容是123。

`var a = "abc"  
a = Number(a);` //a是一個數值，內容是NaN。

`var a = "   ";  
a = Number(a);` //a是一個數值，內容是0。



#### 布林

* true轉1，false轉0。

範例：

`var a = true;  
a = Number(a);` //a是一個數值，內容是1。



#### null與undefined

* null轉數字0。
* undefined轉為NaN。

範例：

`var a = null;  
a = Number(a);` //a是一個數值，內容是0。

`var a = undefined;  
a = Number(a);` //a是一個數值，內容是NaN。
{% endtab %}

{% tab title="parse\(\);" %}
### 方法二－`parseInt();  parseFloat();`  //這是函數

專門針對字串轉數值。

* parseInt\(\)  轉換為整數
* parseFloat\(\)轉換為浮點數

範例：

`var a = "123.2a3px";  
a = parseInt(a);` //a為數值，內容為123

`var a = "b123.2";  
a = parseInt(a);` //a為數值，內容為NaN

`var a = "123.2a3px";  
a = parseFloat(a);` //a為數值，內容為123.2
{% endtab %}
{% endtabs %}

## 其他進位數

{% tabs %}
{% tab title="16進位" %}
### 16進位用「`0x`」開頭

`a = 0x10;` //a數值為16

`a = 0xff;` //a數值為255

`a = 0xCafe;` //a數值為51966
{% endtab %}

{% tab title="8進位" %}
### 8進位用「`0`」開頭

`a = 070;` //a數值為56
{% endtab %}

{% tab title="2進位" %}
### 2進位用「`0b`」開頭
{% endtab %}

{% tab title="對應關係" %}
| 十進位 | 二進位 | 八進位 | 十六進位 | 十進位 | 二進位 | 八進位 | 十六進位 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | 0 | 0 | 0 | 10 | 1010 | 12 | A |
| 1 | 1 | 1 | 1 | 11 | 1011 | 13 | B |
| 2 | 10 | 2 | 2 | 12 | 1100 | 14 | C |
| 3 | 11 | 3 | 3 | 13 | 1101 | 15 | D |
| 4 | 100 | 4 | 4 | 14 | 1110 | 16 | E |
| 5 | 101 | 5 | 5 | 15 | 1111 | 17 | F |
| 6 | 110 | 6 | 6 | 16 | 10000 | 20 | 10 |
| 7 | 111 | 7 | 7 | 17 | 10001 | 21 | 11 |
| 8 | 1000 | 10 | 8 | 18 | 10010 | 22 | 12 |
| 9 | 1001 | 11 | 9 | 19 | 10011 | 23 | 13 |
{% endtab %}

{% tab title="回推" %}
回推

`parseInt('31',16);` //16進位的31。他的10進位是多少？結果是「49」
{% endtab %}
{% endtabs %}

## 

