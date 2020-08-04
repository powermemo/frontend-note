# 運算式

## 運算、算數、比較運算子

運算、比較運算子很基本跳過w。

* ++ \| -- 在前，先改變變數值、再執行運算式
* ++ \| -- 在後，先執行運算式、再改變變數值

{% tabs %}
{% tab title="範例1" %}
```php
<?php
$x = 10;
$y = ++$x + 5;
echo "x : $x <br>"; //11
echo "y : $y <br>"; //16
//-----------------------
$x = 10;
$y = $x++ + 5;
echo "x : $x <br>"; //11
echo "y : $y <br>"; //15
?>
```
{% endtab %}

{% tab title="範例2" %}
```php
<?php
$a = 10;
$b = ++$a + ++$a; //a:11,12 ,(11+12)
echo "a : $a <br>"; //12
echo "b : $b <br>"; //23
//-----------------------
$a = 10;
$b = $a++ + $a++; //(10+11) a:11,12
echo "a : $a <br>"; //12
echo "b : $b <br>"; //21
?>
```
{% endtab %}
{% endtabs %}

## 邏輯運算子

| A | B | A and B | A or B | A xor B |
| :--- | :--- | :--- | :--- | :--- |
| T | T | T | T | F |
| T | F | F | T | T |
| F | T | F | T | T |
| F | F | F | F | F |

{% hint style="info" %}
xor：連結兩運算元，其值不同為true，其值相同為false。  
ex.AB都是T，AxorB就是false；A是T、B是F，AxorB就是true。  
ex.AB都是F，AxorB也是false；A是F、B是T，AxorB也是true。
{% endhint %}

## 字串結合運算子「.」

相當於JS的「+」。

```php
<?php
echo "name: "."amy";
?>
```

## 三元運算子「? : 」

這部分跟JS一樣。

```php
//跟JS一樣。
<?php
$avg = 86;
echo $avg>60?'pass!':'LOSER!';
//變數avg大於60嗎？如果是大於60就印出「pass!」；若不是大於60就印出「LOSER!」
?>
```

## 錯誤控制運算子「@」

```php
<?php
$x = 10;
$y = 0;
echo @($x/$y);//🔶will NOT print
?>
```

