---
description: 分為自訂函式與內建函式
---

# 函數

## 內建函式

* 數學
* 字串
* 陣列
* 日期 \[[官網連結](https://www.php.net/manual/en/function.date)\]
* mySQL
* PHP相關資訊
* 目錄管理
* 檔案系統
* 電子郵件
* ...

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x6578;&#x5B57;</th>
      <th style="text-align:left">&#x5B57;&#x4E32;</th>
      <th style="text-align:left">&#x65E5;&#x671F;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>&#x4E82;&#x6578;</p>
        <p><code>rand()</code>
        </p>
      </td>
      <td style="text-align:left">
        <p>&#x5B57;&#x4E32;&#x9577;&#x5EA6;</p>
        <p><code>strlen($str)</code>
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>&#x66F4;&#x597D;&#x7684;&#x4E82;&#x6578;</p>
        <p><code>mt_rand()</code>
        </p>
      </td>
      <td style="text-align:left">
        <p>&#x5728;&#x5B57;&#x4E32;&#x4E2D;&#x7684;&#x4F4D;&#x7F6E;</p>
        <p><code>strpos($str, &quot;&#x5B57;&#x4E32;&quot;)</code>
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>&#x53D6;&#x5C0F;&#x65BC;x&#x7684;&#x6700;&#x5927;&#x6574;&#x6578;</p>
        <p><code>floor()</code>
        </p>
      </td>
      <td style="text-align:left">
        <p>&#x53D6;&#x5B50;&#x5B57;&#x4E32;</p>
        <p><code>substr($str,&#x5F9E;&#x54EA;&#x958B;&#x59CB;,&#x53D6;&#x5E7E;&#x500B;&#x5B57;)</code>
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>&#x53D6;&#x5927;&#x65BC;x&#x7684;&#x6700;&#x5C0F;&#x6574;&#x6578;</p>
        <p><code>ceil()</code>
        </p>
      </td>
      <td style="text-align:left">
        <p>&#x5207;&#x5B57;&#x4E32;&#x1F538;&#x6703;&#x8B8A;&#x6210;&#x9663;&#x5217;</p>
        <p><code>explode(&quot;&#x7528;&#x751A;&#x9EBC;&#x5207;&#x5B57;&#x4E32;,&quot;$str)</code>
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>&#x9023;&#x63A5;&#x5B57;&#x4E32;</p>
        <p><code>implode(&quot;&#x7528;&#x751A;&#x9EBC;&#x9023;&#x63A5;&#x5B57;&#x4E32;,&quot;$&#x5F88;&#x591A;&#x5B57;&#x4E32;&#x53EF;&#x80FD;&#x662F;&#x9663;&#x5217;)</code>
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

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
echo 'strlen($str): ', strlen($str),"<br>";//10
echo 'strpos($str,"cd"): ', strpos($str,"cd"),"<br>";//2
echo 'strpos($str,"eab"): ', strpos($str,"eab"),"<br>";//4
echo 'substr($str,2,5): ', substr($str,2,5),"<br>";//cdeab
echo "<b>EXPLODE</b><br>";
$str = 'aa,bb:cc,dd,ee';
$arr = explode(",",$str);//🟡explode()is an array
foreach($arr as $i => $data){//0:aa 1:bb:cc 2:dd 3:ee
	echo "$i : $data <br>";
}

$arr = array(11,22,33);
echo "<b>JOIN: </b>",implode(",",$arr), "<br>";//11,22,33
```
{% endtab %}

{% tab title="英文以外的字串" %}
```php
$str = '日月金木水火土';
echo 'mb_strlen($str): ',mb_strlen($str),"<br>";//7
echo 'mb_strpos($str,"金"): ',mb_strpos($str,"金"),"<br>";//2
echo 'mb_substr($str,2,5): ',mb_substr($str,2,5),"<br>";//金木水火土
```
{% endtab %}

{% tab title="字串練習" %}
```php
$tit = '作業練習-標題只要十個字，若>10個字就取7個字+「...」';
if(mb_strlen($tit) > 10){
	echo mb_substr($tit,0,7),'...<br>';
}else{
	echo $tit,"<br>";
}//作業練習-標題...

//三元運算寫法
echo (mb_strlen($tit) > 10) ? mb_substr($tit,0,7).'...<br>' : $tit,"<br>";
//🟡「?」及「:」中間的字串串接要用「.」，不然會error
```
{% endtab %}

{% tab title="日期函數" %}
```php
<h2>time(), date(), mktime()</h2>
<?php
echo "now: ", time(),"<br>";//now: 1594862700
$now = time();
echo "time: ", date("Y-m-d H:i:s",$now),"<br>";//time: 2020-07-16 09:25:00
echo "time: ", date("Y-m-d H:i:s"),"<br>";//time: 2020-07-16 09:25:00
$birthday = mktime(0,0, 0, 1, 5, 1985);
echo date("星期:w",$birthday), "<br>";//weekday: 4
//https://www.php.net/manual/en/function.date
?>
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
【非英文字串】使用「mbstring」。預設是關的，要打開....

1. php.ini找「extension=mbstring」，並把「;」註解拿掉
2. php.ini找「extension\_dir="ext"」，把「;」註解拿掉 將等號後面的值改為資料夾位置ex.「C:\php-7.4.7\ext」
3. 打開IIS，重新啟動。
{% endhint %}



