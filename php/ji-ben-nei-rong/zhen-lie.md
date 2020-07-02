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
	echo "$i : $data<br>";
}
```
{% endtab %}
{% endtabs %}



