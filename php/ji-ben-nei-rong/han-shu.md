---
description: 分為自訂函式與內建函式
---

# 函式

## 內建函式

* 數學
* 字串
* 陣列
* 日期 \[[官網連結](https://www.php.net/manual/en/function.date)]
* mySQL
* PHP相關資訊
* 目錄管理
* 檔案系統
* 電子郵件
* ...

| 數字                                          | 字串                                                                       | 日期                                                 |
| ------------------------------------------- | ------------------------------------------------------------------------ | -------------------------------------------------- |
| <p>亂數</p><p><code>rand()</code></p>         | <p>字串長度</p><p><code>strlen($str)</code></p>                              | <p>現在時間</p><p><code>time()</code></p>              |
| <p>更好的亂數</p><p><code>mt_rand()</code></p>   | <p>在字串中的位置</p><p><code>strpos($str, "字串")</code></p>                     | <p>時間格式</p><p><code>date("格式", 時間函式等)</code></p>   |
| <p>取小於x的最大整數</p><p><code>floor()</code></p> | <p>取子字串</p><p><code>substr($str,從哪開始,取幾個字)</code></p>                    | <p>時間戳記</p><p><code>mktime(時,分,秒,月,日,年)</code></p> |
| <p>取大於x的最小整數</p><p><code>ceil()</code></p>  | <p>切字串🟡會變成陣列【字串轉陣列】</p><p><code>explode("用甚麼切字串,"$str)</code></p>       |                                                    |
|                                             | <p>連接字串【(可能是)陣列轉字串】</p><p><code>implode("用甚麼連接字串,"$很多字串可能是陣列)</code></p> |                                                    |
|                                             | <p>英文外的字串，以🟡「mb_」開頭</p><p>例如字串長度：<code>mb_strlen($str)</code></p>       |                                                    |

{% tabs %}
{% tab title="數學" %}
```php
echo "floor(2.4): ",floor(2.4), "<br>";//2，無條件捨去
echo "ceil(2.4): ",ceil(2.4), "<br>";//3，無條件進位
echo "ceil(28/7): ",ceil(28/7), "<br>";//4
```
{% endtab %}

{% tab title="字串" %}
```php
$str = 'abcdeabcde';
echo 'strlen($str): ', strlen($str),"<br>";//10，字串長杜
echo 'strpos($str,"cd"): ', strpos($str,"cd"),"<br>";//2，字串位置
echo 'strpos($str,"eab"): ', strpos($str,"eab"),"<br>";//4，字串位置
echo 'substr($str,2,5): ', substr($str,2,5),"<br>";//cdeab，取子字串

//=====EXPLODE切字串=====【字串轉陣列】
$str = 'aa,bb:cc,dd,ee';
$arr = explode(",",$str);//🟡explode()是一個陣列
foreach($arr as $i => $data){//0:aa 1:bb:cc 2:dd 3:ee
	echo "$i : $data <br>";
}

//=====IMPLODE連接字串=====【(可能是)陣列轉字串】
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


//生日那天星期幾？(用1985/01/05作範例)
$birthday = mktime(0,0, 0, 1, 5, 1985);
echo date("星期:w",$birthday), "<br>";//星期: 6
?>
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
【非英文字串】使用「mbstring」。預設是關的，要打開....

1. php.ini找「extension=mbstring」，並把「;」註解拿掉
2. php.ini找「extension\_dir="ext"」，把「;」註解拿掉\
   將等號後面的值改為資料夾位置ex.「C:\php-7.4.7\ext」
3. 打開IIS，重新啟動。
{% endhint %}

{% hint style="info" %}
三元運算，「?」及「:」中間的字串串接要用「.」，不然會error
{% endhint %}

## 自訂函式

{% tabs %}
{% tab title="簡單起始" %}
```php
function sum($a, $b){
	$total = 0;
	$total = $a + $b;
	return $total;
}
echo "10+20 = ", sum(10,20), "<br>";//10+20=30



function sayHello($name){
	echo "Hello",$name,"<br>";
}
sayHello("Alice");//Hello Alice
```
{% endtab %}

{% tab title="參數可以是陣列" %}
```php
function sumMany($array){//$array: 請將所有的資料放到陣列中...
	$total = 0;
	if(is_array($array)){foreach($array as $data){$total += $data;}}
	else{return false;}
	return $total;
}
$arr = array(10,20,30);
echo "10+20+30=", sumMany($arr),"<br>";
/*自訂函數的參數值可以定義陣列(可用foreach帶)。
 *但參數一定要式陣列型態，不然你可以寫if_else讓程式辨別，非陣列型態要return false*/
//PHP的自訂函數不可以重複命名！(JS可以)
```
{% endtab %}
{% endtabs %}

{% hint style="danger" %}
PHP的自訂函數不可以重複命名！(JS可以)
{% endhint %}

{% hint style="info" %}
*   自訂函數的參數值可以定義陣列(可用foreach帶)。

    但參數一定要是陣列型態，不然你可以寫else讓程式辨別，非陣列型態要return false
{% endhint %}



### 傳值呼叫 & 傳址呼叫

{% tabs %}
{% tab title="簡單起始" %}
```php
<h2>call by value</h2>
<?php
function sum_test1($a,$b){
	$total = $a + $b;
	$a += 100;
	$b += 100;
	return $total;
}
$x = 10;
$y = 20;
echo "x + y =", sum_test1($x,$y), "<br>";//x + y =30
echo "x = $x <br>";											//x = 10
echo "y = $y <br>";											//y = 20
?>

//====================================================

<h2>call by reference</h2>
<?php
function sum_test2(&$a,&$b){//🟡參數變數前面有加「&」
	$total = $a + $b;
	$a += 100;
	$b += 100;
	return $total;
}
$x = 10;
$y = 20;
echo "x + y =", sum_test2($x,$y), "<br>";//x + y =30
echo "x = $x <br>";											//x = 110
echo "y = $y <br>";											//y = 120
?>
```
{% endtab %}

{% tab title="範例-加薪" %}
```php
//薪水加薪
<h4>call by value</h4>
<?php
function adjustSalary_pp($dataArr,$amt){
	for($i=0;$i<count($dataArr);$i++){
		$dataArr[$i] += $amt;
	}
	return $dataArr;														//🟡
}
$salaryArr = array(10000,20000,30000,40000);
$salaryArr = adjustSalary_pp($salaryArr,2000);//🟡
print_r($salaryArr);
//12000  22000  32000  42000
?>

//====================================================

<h4>call by reference</h4>
<?php
function adjustSalary_pp2(&$dataArr,$amt){//🟡
	for($i=0;$i<count($dataArr);$i++){
		$dataArr[$i] += $amt;
	}
}
$salaryArr = array(10000,20000,30000,40000);
adjustSalary_pp2($salaryArr,2000);				//🟡
print_r($salaryArr);

?>
```
{% endtab %}

{% tab title="範例" %}
```php
<h2>salary array每人加薪</h2>
<?php
function adjustSalary(&$dataArr,$amt){//🟡
	for($i=0;$i<count($dataArr);$i++){
		$dataArr[$i] += $amt;
	}
	return $dataArr;
}
$salaryArr = array(10000,20000,30000,40000);
adjustSalary($salaryArr,2000);
foreach($salaryArr as $i => $data){
	echo "$data <br>";
}
?>
```
{% endtab %}
{% endtabs %}

### 設定參數的預設值

```php
<h2>預設參數</h2>
<?php
function printMark($classId="前端工程師班級..."){//🟡
	echo "*****<br>";
	echo "*****<br>";
	echo "*****<br>";
	echo "*****<br>";
	echo "*****<br>";
	echo "*****<br>$classId<br>";
}
echo printMark("ED102");
//echo printMark();

?>
```

### 區域變數  全域變數  靜態變數

{% tabs %}
{% tab title="全域變數global " %}
```php
<h2>global</h2>
<?php
$amount = 0;					//全域變數
function getAmount(){//程式中使用到的amount是使用全域變數(上面定義=0的那個)
	global $amount;		//🟡全域equal as ===> $GLOBALS["amount"];
	//...
	//...
	$amount = 100000;	//全域
}

function showAmount(){
global $amount;			//全域equal as ===> $GLOBALS["amount"];
	echo "<h3 style='color:blue;'>total: ", $amount ,"</h3><br>";
}

getAmount();
showAmount();
?>
```
{% endtab %}

{% tab title="靜態變數static" %}
```php
<h2>static</h2>
<?
function myStatic(){
	static $i = 0; //靜態變數
	$i += 1;
	return $i;
}
echo myStatic(),"<br>";//1
echo myStatic(),"<br>";//2, 靜態變數的值不會被清空, 會繼續計算
?>
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
* 與JS不同，PHP的function變數不會往外找全域變數。\
  必須在function內告訴程式(例如global $...)，程式才會往外抓變數。
* 靜態變數的值不會被清空, 會繼續計算
{% endhint %}
