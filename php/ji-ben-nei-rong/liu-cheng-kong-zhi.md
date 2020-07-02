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
{% endtabs %}

