---
description: 分為自訂函式與內建函式
---

# 函數

## 內建函式

* 數學
* 字串
* 陣列
* 日期
* mySQL
* PHP相關資訊
* 目錄管理
* 檔案系統
* 電子郵件
* ...

{% tabs %}
{% tab title="數學" %}
```php
echo "floor(2.4): ",floor(2.4), "<br>";//2
echo "ceil(2.4): ",ceil(2.4), "<br>";//3
echo "ceil(28/7): ",ceil(28/7), "<br>";//4
```
{% endtab %}

{% tab title="字串" %}
```php
$str = 'abcdeabcde';
echo 'strlen($str): ', strlen($str),"<br>";
echo 'strpos($str,"cd"): ', strpos($str,"cd"),"<br>";
echo 'strpos($str,"cdd"): ', strpos($str,"cdd"),"<br>";
echo 'substr($str,2,5): ', substr($str,2,5),"<br>";
echo "<b>EXPLODE</b><br>";
$str = 'aa,bb:cc,dd,ee';
$arr = explode(",",$str);//🔸explode()is an array
foreach($arr as $i => $data){
	echo "$i : $data <br>";
}

$arr = array(11,22,33);
echo "<b>JOIN: </b>",implode(",",$arr), "<br>";
```
{% endtab %}
{% endtabs %}

