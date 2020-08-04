---
description: 一種資料交換的格式
---

# JSON

## HTML的JSON

{% hint style="info" %}
兩種常見的方法

* `JSON.stringify(js物件)`
* `JSON.parse(json字串)`
{% endhint %}

對應範例檔0804「json.html」

{% tabs %}
{% tab title="stringify" %}
JSON.stringify\(js物件\)

```javascript
var emp={empno: "7001",ename: "Andy",sal: 33000,}
var str = JSON.stringify(emp);                    //🟡
document.write("json:",str,"<br>");
//【result】json:{"empno":"7001","ename":"Andy","sal":33000}
```
{% endtab %}

{% tab title="Second Tab" %}

{% endtab %}
{% endtabs %}

## PHP的JSON

對應範例檔0804「json.php」

{% tabs %}
{% tab title="First Tab" %}

{% endtab %}

{% tab title="Second Tab" %}

{% endtab %}
{% endtabs %}

