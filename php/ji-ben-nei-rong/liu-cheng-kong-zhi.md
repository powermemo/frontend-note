# 流程控制

跟JS很像..

花括號PHP有替代寫法

{% tabs %}
{% tab title="if" %}
```php
if(條件){
    敘述;
}elseif(條件){
    敘述;
}[else{
    敘述;
}]
//中括號表optional

//--------------------以下式取代花括號的方式

if(條件):
    敘述;
elseif(條件):
    敘述;
[else:
    敘述;
}]
endif;
```
{% endtab %}

{% tab title="switch" %}
```php
switch(運算式){
    case 值1:
        敘述;
        [break;]
    case 值2:
        敘述;
        [break;]
...
    case 值n:
        敘述;
        [break;]
    [default:
        敘述;]
}

//--------------------以下式取代花括號的方式

switch(運算式):
    case 值1:
        敘述;
        [break;]
    case 值2:
        敘述;
        [break;]
...
    case 值n:
        敘述;
        [break;]
    [default:
        敘述;]
endswitch;
```
{% endtab %}

{% tab title="for" %}
```php
//通常for迴圈的「break」會搭配if條件式(不然做一次就停啦==)。
$total = 0;
for($i=0;$i<=1000;$i++){
	$total = $total + $i;
	if($total > 1000){
		echo '1+2+...+$i =' ,$total,
			'will large than 1000';
		break;//結束for迴圈
	}
}
```
{% endtab %}

{% tab title="while" %}
```php
$total = 0;
$i=0;
while($i<=1000){
	$total = $total + $i;
	$i++;
	if($total > 1000){
		echo '1+2+...+$i =' ,$total,
			'will large than 1000';
		break;//end loop
	}
}
```
{% endtab %}
{% endtabs %}

## 作業練習

{% tabs %}
{% tab title="PHP1" %}
```php
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
```
{% endtab %}

{% tab title="PHP2" %}
```php
/* 摸彩金 : 有11顆彩球, 彩球面額為0-10之間, 
 * 若摸到的彩球不為0,則可繼續摸彩,若摸到的彩球為0,則停止摸彩,
 * 並計算其摸彩次數及彩金總金額(單位:佰元) 
*/
$i = 0;
do{
	$ball[$i] = rand(0,10);
	foreach($ball as $m => $data);
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
```
{% endtab %}
{% endtabs %}

