# 陣列

## 新增陣列

{% tabs %}
{% tab title="array\(\)" %}
```php
//PHP的「count()」相當於JS的「.length」
<?php
$arr = array(11,22,33);
for($i=0;$i<count($arr);$i++){
	echo $arr[$i]," ";
}
?>
```
{% endtab %}

{% tab title="一一指定" %}
```php
$arr2[0] = 10;
$arr2[1] = 20;
$arr2[] = 30;
$arr2[] = 40;
$arr2[1] = 100;
for($i=0;$i<count($arr2);$i++){
	echo $arr2[$i]," ";
}
```
{% endtab %}
{% endtabs %}

## foreach\(as\)

PHP可以`$arr[5]='測試字串';`一一指定陣列的值，但\[0\]~\[4\]都沒有給值，PHP不會保留位置  
這時候若使用「for」迴圈去echo\(印出\)資料，會出現錯誤訊息。

為了排除錯誤訊息，要使用「foreach\(as\)」找出對印的陣列位置及資料。  
語法：  
`foreach($陣列名稱 as [$鍵值變數名稱 =>] $資料變數名稱)`  
foreach\($zip as $key =&gt;  $data\)

{% tabs %}
{% tab title="錯誤訊息" %}
```php
$arr3[] = "a";//index[0]==>'a'
$arr3[] = "b";//index[1]==>'b'
$arr3[1] = "c";//index[1]==>'c'
$arr3[] = "d";//index[2]==>'d'
$arr3[6] = "e";//index[6]==>'e'
//🔶🔷PHP不會保留[3][4][5]的位置，但JS會
//🔶🔶<count($arr3)錯誤，因為[3][4][5]沒有資料
for($i=0;$i<count($arr3);$i++){
	echo $arr3[$i]," ";
}
```
{% endtab %}

{% tab title="foreach\(as\)" %}
```php
$arr3[] = "a";//index[0]==>'a'
$arr3[] = "b";//index[1]==>'b'
$arr3[1] = "c";//index[1]==>'c'
$arr3[] = "d";//index[2]==>'d'
$arr3[6] = "e";//index[6]==>'e'
//PHP不會保留[3][4][5]的位置，但JS會

//🔶🔶🔶🔶🔶
//$i和$data是自定義的，沒有一定要這樣命名。
foreach($arr3 as $i => $data){
	echo "index[$i] : $data<br>";
}
```
{% endtab %}
{% endtabs %}

## 相關函數

| 函數 | 作用 |
| :--- | :--- |
| count\(陣列變數\) | 傳回陣列中元素的個數 |
| print\_r\(陣列變數\) | 顯示陣列中的所有資料 |
| is\_array\(變數\) | 檢視變數中的資料是否維陣列？ |
| in\_array\(要搜尋的值,陣列變數\) | 傳回資料是否在陣列中？ |
| array\_search\(要搜尋的值,陣列變數\) | 傳回資料在陣列中的 索引值 |
| shuffle\(陣列變數\) | 將陣列中的資料打亂 |
|  |  |

{% tabs %}
{% tab title="print\_r" %}
```text

```
{% endtab %}
{% endtabs %}

