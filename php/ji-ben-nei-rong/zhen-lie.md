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

{% tab title="關係陣列" %}
```php
//一維關係陣列
$classmate = array('01'=>'Ling', '02'=>'Wendy','03'=>'nn');
$classmate["04"] = "Cloud";//另一種新增方式
foreach($classmate as $id => $data){
	echo "id: $id, name: $data<br>";
};
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
| array\_sum\(陣列變數\) |  |
| array\_values\(陣列變數\) |  |
| ... |  |

{% tabs %}
{% tab title="print\_r" %}
```php
$classmate = array('01'=>'Ling', '02'=>'Wendy','03'=>'nn');
$classmate["04"] = "Cloud";
print_r($classmate);
//Array ( [01] => Ling [02] => Wendy [03] => nn [04] => Cloud )
```
{% endtab %}

{% tab title="is\_array" %}
```php
$arr = 10;
$arr2 = array(11,22,33);
echo 'is_array($arr):', is_array($arr), "<br>";//空值
echo 'is_array($arr2):', is_array($arr2), "<br>";//1
```
{% endtab %}

{% tab title="in\_array" %}
```php
$arr2 = array(11,22,33);
echo 'in_array(33,$arr):', in_array(33, $arr2), "<br>";//1
echo 'in_array(333,$arr2):', in_array(333, $arr2), "<br>";//空值
```
{% endtab %}

{% tab title="array\_search" %}
```php
$arr2 = array(11,22,33);
echo 'array_search(33,$arr):', array_search(33, $arr2), "<br>";//2
echo 'array_search(333,$arr2):', array_search(333, $arr2), "<br>";//空值
```
{% endtab %}

{% tab title="shuffle洗牌" %}
```php
$arr = array('aa','bb','cc','dd','ee','ff');
print_r($arr); echo'<br>';
shuffle($arr);
print_r($arr);
```
{% endtab %}
{% endtabs %}

## 作業練習

```php
<?php
/*隨機產生10個介於1-~100之間的數放在陣列中, 
印出這10個數, 總和 , 最小值 , 最大值
*/

for($i=0;$i<10;$i++){
	$arr[$i] = rand(1,100);
}
//$min = min($arr); //作弊手法XD
//$max = max($arr); //作弊手法XD
$min = 101;
$max = 0;
foreach($arr as $p => $data){
	for($j=0;$j<count($arr);$j++){
		if($min > $arr[$j]){$min = $arr[$j];}
		if($max < $arr[$j]){$max = $arr[$j];}
	}
}


echo '所有陣列：';
print_r($arr);//the ten of numbers
echo '<h1>隨機產生10個介於1-~100之間的數放在陣列中, <br>
	印出這10個數, 總和 , 最小值 , 最大值</h1>'.
	'<h2>答案如下</h2>';
foreach($arr as $p => $data){
	echo "<br>第[", $p + 1 ,"]個 － $data";
};

echo '<br>總和：',array_sum($arr),'<br>';//numbers' sum
echo '最小值：',$min,'<br>';
echo '最大值：',$max;
?>
```

