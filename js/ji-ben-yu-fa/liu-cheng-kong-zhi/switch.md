# switch

各種選擇，但不能用於精確數值，因為JS是浮點數，意思是我打1，程式裡卻是1.0。

從第一個匹配到的「case」執行，一直到遇到「break」後，停止執行。  
如果沒有「break」，JS會繼續往下一行執行。  
當程式找不到可以匹配「case」，就會去找「default」。  
大概是這樣的寫法...

{% tabs %}
{% tab title="case不同值" %}
```javascript
switch(lowercaseLetter) { //小括號內是你要比對的東西
  case "a":
    console.log("A");
    break;
  case "b":
    console.log("B");
    break;
...
  default:
    defaultStatement;
    break;
}
```
{% endtab %}

{% tab title="多case相同值" %}
```javascript
switch(val) {
  case 1:
  case 2:
  case 3:
    result = "1, 2, or 3";
    break;
  case 4:
    result = "4 alone";
}
```
{% endtab %}

{% tab title="比較if和switch" %}
```javascript
/*兩個寫法是一樣的結果～～～*/
//首先是if else
if (val === 1) {
  answer = "a";
} else if (val === 2) {
  answer = "b";
} else {
  answer = "c";
}


//然後是switch
switch(val) {
  case 1:
    answer = "a";
    break;
  case 2:
    answer = "b";
    break;
  default:
    answer = "c";
}
```
{% endtab %}
{% endtabs %}

