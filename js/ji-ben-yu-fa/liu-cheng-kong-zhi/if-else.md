---
description: 是個看順序的傢伙
---

# if else

## if

## if else

{% tabs %}
{% tab title="舉例寫法" %}
```javascript
if (num > 10) {
  return "Bigger than 10";
} else {
  return "10 or Less";
}
```
{% endtab %}

{% tab title="比較好笑的寫法" %}
```javascript
//我用了兩個if
if (num > 10) {
  return "Bigger than 10";
} 
if (num <= 10) {
  return "10 or Less";
}
```
{% endtab %}
{% endtabs %}

## if else if else

當我的條件有兩個以上時，中間就使用「elseif」，  
請留意，**「else」一直都是墊底的角色**w（因為是最後，所以可以不用給它條件判斷）。  
然而「else」是選填的😆

寫法～  
`if(條件){執行};` 　　//第一個判斷  
`else if(條件){執行};` //第二個判斷  
`else if(條件){執行};` //第三個判斷  
`else if(條件){執行};` //第四個判斷  
//反正就是很多else if\(\){};  
`else{執行};`　   //最後一個判斷





