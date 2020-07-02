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

