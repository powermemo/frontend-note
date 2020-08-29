# 陣列

## 新增陣列

{% tabs %}
{% tab title="直接指定" %}
```php
$arr2[0] = 10;
$arr2[1] = 20;
$arr2[] = 30;  //系統幫忙帶入$arr2[2] = 30;
$arr2[] = 40;  //系統幫忙帶入$arr2[3] = 40;
$arr2[1] = 100;
for($i=0;$i<count($arr2);$i++){
	echo $arr2[$i]," ";
}
```
{% endtab %}

{% tab title="array\(\)" %}
```php
//PHP的「count()」相當於JS的「.length」
$arr = array(11,22,33);
for($i=0;$i<count($arr);$i++){
	echo $arr[$i]," ";  //跟JS一樣，陣列索引值可以是變數
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
PHP的「count\(\)」相當於JS的「.length」。  
跟JS一樣，PHP陣列索引值可以是變數
{% endhint %}

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

{% hint style="info" %}
上例，PHP不會保留\[3\]\[4\]\[5\]的位置，但JS會  
&lt;count\($arr3\)錯誤，因為\[3\]\[4\]\[5\]沒有資料
{% endhint %}

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
//顯示所有資料
$classmate = array('01'=>'Ling', '02'=>'Wendy','03'=>'nn');
$classmate["04"] = "Cloud";
print_r($classmate);
//Array ( [01] => Ling [02] => Wendy [03] => nn [04] => Cloud )
```
{% endtab %}

{% tab title="is\_array" %}
```php
//檢測資料是否為陣列
$arr = 10;
$arr2 = array(11,22,33);
echo 'is_array($arr):', is_array($arr), "<br>";//空值
echo 'is_array($arr2):', is_array($arr2), "<br>";//1
```
{% endtab %}

{% tab title="in\_array" %}
```php
//在陣列中嗎？
$arr2 = array(11,22,33);
echo 'in_array(33,$arr):', in_array(33, $arr2), "<br>";//1
echo 'in_array(333,$arr2):', in_array(333, $arr2), "<br>";//空值
```
{% endtab %}

{% tab title="array\_search" %}
```php
//傳回資料在陣列中的索引值
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

## 作業練習－摸彩

{% tabs %}
{% tab title="" %}
```php
<?php
/*摸彩金 : 有11顆彩球, 彩球面額為0-10之間, 
 *可以摸彩10次, 印出其每次的摸彩金額及彩金總金額(單位:佰元)*/
for($i=0;$i<11;$i++){
	$ball[$i] = rand(0,10);
}
print_r($ball);
echo "<h1>摸彩金 : 有11顆彩球, 彩球面額為0-10之間, <br>
	 可以摸彩10次, 印出其每次的摸彩金額及彩金總金額(單位:佰元)</h1>".
 	"<h2>答案如下</h2>";
foreach($ball as $p => $data){
	echo "$ ",$data * 100,"<br>";
};
echo "<br>總額：$ " ,array_sum($ball) * 100;
?>
```
{% endtab %}

{% tab title="" %}
```php
<?php
/* 摸彩金 : 有11顆彩球, 彩球面額為0-10之間, 
 * 若摸到的彩球不為0,則可繼續摸彩,若摸到的彩球為0,則停止摸彩,
 * 並計算其摸彩次數及彩金總金額(單位:佰元) 
*/
$i = 0;
do{
	$ball[$i] = rand(0,10);
	//foreach($ball as $m => $data);
	//如果數字是零就結束(無法再摸彩)
	if($ball[$i]==0){break;}
	else{$i++;}
}while($i<10);

echo '所有陣列';
print_r($ball);
echo "<h1>摸彩金 : 有11顆彩球, 彩球面額為0-10之間, <br>
 	若摸到的彩球不為0,則可繼續摸彩,若摸到的彩球為0,則停止摸彩,<br>
 	並計算其摸彩次數及彩金總金額(單位:佰元) ".
	"<h2>答案如下</h2>";
foreach($ball as $p => $data){
	echo "$ ",$data * 100,"<br>";
};
echo "<br>總額：$ " ,array_sum($ball) * 100;

?>
```
{% endtab %}

{% tab title="PHP" %}
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
{% endtab %}
{% endtabs %}

## 二維陣列

{% tabs %}
{% tab title="新建" %}
```php
//方法1️⃣先建立一維陣列，再建立二微陣列
$row0 = array(83,85);
$row1 = array(79,77);
$row2 = array(95,91);
$score = array($row0, $row1, $row2);

//方法2️⃣直接建立二維陣列
$score = (array(83,85), array(79,77), array(95,91));
```
{% endtab %}

{% tab title="初試" %}
```php
$arr = array(array(1,2,3,4),11,true, 'this is a book');

//echo $arr[0];//[🚫not allow print array!][you need to turn it be string] //print_r()is okay!
echo $arr[0][3];//4
echo $arr[2];//true
echo $arr[3];//this is a book
```
{% endtab %}

{% tab title="for" %}
以下表格是印出結果。

| 1 | 2 | 3 | 4 |
| :--- | :--- | :--- | :--- |
| 11 | 12 | 13 | 14 |
| 21 | 22 | 23 | 24 |

```php
$arr = array(array(1,2,3,4),array(11,12,13,14),array(21,22,23,24));
echo "<table align='center' cellspacing='0' border='1'>";
for($i=0;$i<3;$i++){
	echo "<tr>";
	for($j=0;$j<4;$j++){
		echo "<td>",$arr[$i][$j],"</td>";
	}
	echo "</tr>";
}
echo "</table>";

```
{% endtab %}

{% tab title="foreach" %}
以下表格是印出結果。

| 1 | 2 | 3 | 4 |
| :--- | :--- | :--- | :--- |
| 11 | 12 | 13 | 14 |
| 21 | 22 | 23 | 24 |

```php
$arr = array(array(1,2,3,4),array(11,12,13,14),array(21,22,23,24));
echo "<table align='center' cellspacing='0' border='1'>";
foreach($arr as $i => $row){
	echo "<tr>";
	foreach($row as $j => $data){
		echo "<td>",$arr[$i][$j],"</td>";
	}
	echo"</tr>";
}
echo "</table>";
```
{% endtab %}

{% tab title="二維陣列表單練習" %}
html+PHP\(檔名：0713arrayForm.php\)

```markup
<form action="0713arrayForm.php">
    帳號<input type="text" name="memId" /><br />
    英文能力<input type="checkBox" name="ability[]" value="read">讀
        <input type="checkBox" name="ability[]" value="listen">聽
        <input type="checkBox" name="ability[]" value="write">寫<br>
    專長<br>
    <select name="specialty[]" size="3" multiple >
        <option value="VB.NET">VB.NET</option>
        <option value="SQL">SQL Server </option>
        <option value="JAVA">JAVA </option>
        <option value="Delphi">Delphi </option>
    </select>     
    <input type="submit" value="送出">
</form>
```

```php
<?php
echo "account:",$_GET["memId"],"<hr>";
echo "lanuage: <br>";
if(isset($_GET["ability"]) === true){//===true可省略
//isset()用以檢查變數是否存在
	foreach($_GET["ability"] as $i => $data){
		echo "$i : $data<br>";
	}
}
echo "<hr>";
echo "specialty:<br>";
if(isset($_GET["ability"])){
	foreach($_GET['specialty'] as $i => $data){
		echo "$i : $data<br>";
	}
}
?>
```

{% hint style="info" %}
`isset()`用以檢查變數是否存在
{% endhint %}
{% endtab %}

{% tab title="二維作業練習－撲克牌" %}
一副撲克牌52張，請將其洗牌後發給4人，並顯示個玩家所得到的點數，如下所示：

| 玩家一 | 37 | 41 | 3 | 20 | 19 | 14 | 48 | 36 | 38 | 5 | 29 | 49 | 8 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 玩家二 | 28 | 1 | 22 | 51 | 25 | 15 | 12 | 30 | 17 | 24 | 27 | 35 | 47 |
| 玩家三 | 31 | 40 | 45 | 46 | 33 | 44 | 13 | 21 | 11 | 23 | 4 | 18 | 39 |
| 玩家四 | 16 | 43 | 42 | 50 | 34 | 52 | 6 | 9 | 10 | 2 | 26 | 7 | 32 |

```php
//以下是我2020/07/25 Sat做的第二版
<style>
td{
	text-align:center;
	font-family:arial;
}
</style>
<?php
//一副撲克牌52張，請將其洗牌後發給4人，並顯示個玩家所得到的點數：
//建立一個陣列值1~52
$poker = array();
for($i=0;$i<52;$i++){
	$poker[$i] = $i + 1;
	//echo $poker[$i];//for test
}
//打亂
shuffle($poker);
//分配給四個玩家
foreach($poker as $i => $data){
	if($data % 4 == 0){
		$player1[$i] = $data;
	}elseif($data % 4 == 1){
		$player2[$i] = $data;
	}elseif($data % 4 == 2){
		$player3[$i] = $data;
	}elseif($data % 4 == 3){
		$player4[$i] = $data;
	}
}
$myArray = array($player1,$player2,$player3,$player4);
?>

<!-- 印出表格資料 -->
<table cellspacing='0' border='1'>
<?php
foreach($myArray as $i => $row){
	echo "<tr><th>Player",$i+1,"</th>";
	foreach($row as $j => $data){
		echo "<td>".$myArray[$i][$j]."</td>";
	}
	echo "</tr>";
}
?>
</table>

```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
範例：  
`$score = (array(83,85), array(79,77), array(95,91));`  
`echo $score[0];`      //❌錯誤，無法印出陣列。若用`print_r($score);`可以  
`echo $score[0][1];`  //85
{% endhint %}

