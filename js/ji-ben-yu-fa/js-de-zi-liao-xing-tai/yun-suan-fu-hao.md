# 運算符號



<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x904B;&#x7B97;&#x5B50;&#x512A;&#x5148;&#x9806;&#x5E8F;</th>
      <th style="text-align:left">&#x63CF;&#x8FF0;</th>
      <th style="text-align:left">&#x7D50;&#x5408;&#x6027;(&#x57F7;&#x884C;&#x9806;&#x5E8F;)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">()&#x3001;[ ]</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x5F9E;&#x5DE6;&#x5230;&#x53F3;</td>
    </tr>
    <tr>
      <td style="text-align:left">++&#x3001;--&#x3001;+(&#x6B63;)&#x3001;-(&#x8CA0;)</td>
      <td style="text-align:left">&#x4E00;&#x5143;&#x904B;&#x7B97;&#x5B50;</td>
      <td style="text-align:left"><b>&#x5F9E;&#x53F3;&#x5230;&#x5DE6;</b>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">*&#x3001;/&#x3001;%&#x3001;+(&#x52A0;)&#x3001;-(&#x6E1B;)</td>
      <td style="text-align:left">&#x7B97;&#x6578;&#x904B;&#x7B97;&#x5B50;</td>
      <td style="text-align:left">&#x5F9E;&#x5DE6;&#x5230;&#x53F3;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>&gt;&#x3001;&gt;=&#x3001;&lt;&#x3001;&lt;=&#x3001;</p>
        <p>==&#x3001;!=&#x3001;===&#x3001;!==</p>
      </td>
      <td style="text-align:left">&#x95DC;&#x4FC2;&#x904B;&#x7B97;&#x5B50;</td>
      <td style="text-align:left">&#x5F9E;&#x5DE6;&#x5230;&#x53F3;</td>
    </tr>
    <tr>
      <td style="text-align:left">&amp;&amp;&#x3001;&amp;&#x3001;!&#x3001;||&#x3001;|</td>
      <td style="text-align:left">&#x908F;&#x8F2F;&#x904B;&#x7B97;&#x5B50;</td>
      <td style="text-align:left">&#x5F9E;&#x5DE6;&#x5230;&#x53F3;</td>
    </tr>
    <tr>
      <td style="text-align:left">? :</td>
      <td style="text-align:left">&#x689D;&#x4EF6;&#x904B;&#x7B97;&#x5B50;</td>
      <td style="text-align:left">&#x5F9E;&#x5DE6;&#x5230;&#x53F3;</td>
    </tr>
    <tr>
      <td style="text-align:left">=&#x3001;+=&#x3001;-=&#x3001;*=&#x3001;/=&#x3001;%=&#x3001;&#x2026;</td>
      <td
      style="text-align:left">&#x6307;&#x5B9A;&#x904B;&#x7B97;&#x5B50;</td>
        <td style="text-align:left"><b>&#x5F9E;&#x53F3;&#x5230;&#x5DE6;</b>
        </td>
    </tr>
  </tbody>
</table>

字串運算子：字串可用"+"將字串串接。

{% hint style="info" %}
以上表格的結合性（執行順序），除了運算子自己的「從左到右」/「從右到左」外；  
優先順序從\(\) \[ \]開始、最後才是「指定運算子」。
{% endhint %}

## 一元運算子++、--

範例：  
`a = a + 1;`  
相當於`a++;`

`b = b - 1;`  
相當於`b--;`

## 算數運算子+-\*/%

+-\*/就是普通的加減乘除

**%是餘數**。例如5%3;， //結果是2\(5除以3餘數為2\)

## 關係運算子&gt;、&gt;=、&lt;、&lt;=、==、!=、===、!==

* ==「等於」
* !=「不等於」
* ===「絕對等於」\(類型也要比對\)
* !==「絕對不等於」\(類型也要比對\)

一些例子：

{% tabs %}
{% tab title="==" %}
```javascript
1   ==  1   // true
1   ==  2   // false
1   == '1'  // true
```
{% endtab %}

{% tab title="===" %}
```javascript
3 ===  3   // true
3 === '3'  // false
//3是Number類型，'3'是String類型。
```
{% endtab %}

{% tab title="!=" %}
```javascript
1 !=  2     // true
1 != "1"    // false
1 != true   // false
0 != false  // false
```
{% endtab %}

{% tab title="!==" %}
```javascript
3 !==  3   // false
3 !== '3'  // true
4 !==  3   // true
```
{% endtab %}
{% endtabs %}

## 邏輯運算子&&、&、!、\|\|、\|

判斷用

* &&「AND」
* \|\|「OR」

```javascript
//關係運算子搭配邏輯運算子
if (num > 5 && num < 10) { //條件是：變數num要>5 同時也要<10。
  return "Yes";
}
return "No";
```

## 指定運算子=、+=、-=、\*=、/=、%=、…

* `=`一個等號並**不是等於**的意思，而是將右方的值「**分配**」\(或是說賦予\)到左方的意思 （所以才說執行順序是由右至左）。 例如`var a = 5;`。

舉例：  
`myVar = myVar + 5;`  
等同於`myvar += 5;`  
相對的  
`myVar = myVar - 5;`  
等同於`myvar -= 5;`  


舉例2：  
`myVar = myVar * 5;`  
等同於`myvar *= 5;`  
相對的  
`myVar = myVar / 5;`  
等同於`myvar /= 5;`  


## 三元運算\(條件運算\)

`條件判斷?true執行這:false執行這`  
用法我覺得很像if else

```javascript
avg = 86;
document.write(avg>=60?'通過':'再努力');
//avg有大於等於60嗎？    是的話寫「通過」   不是的話寫「再努力」
```

