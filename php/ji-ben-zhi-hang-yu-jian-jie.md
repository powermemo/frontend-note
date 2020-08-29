# 基本執行

## 架構

```php
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>架構模式</title>
</head>
<body>
    <?php
        //單行註解
        /*多行註解*/
        變數宣告;
        函式宣告;
        敘述;        
        echo 'Hello World!';
    ?>
</body>
</html>
```

## 格式

這個是敘述  


* 用`<?php?>`包住
* 用`echo`為起始，後面加入內容

```php
<?php
    echo 'Hello World!';//字串
    echo '<br>';//HTML標籤
    echo 'Hi<br>';//字串+HTML標籤
    echo date('y-m-d h:i:s');//時間
?>
```

下面是內嵌寫法，相當於`<script src=""></script>`

```php
<?php
        include('link.inc')//連結到['link.inc']的檔案
?>
```

{% hint style="info" %}
inc的寫法好比.js檔案，就只要標籤\(如`<h2></h2>`\)、`<?php?>`之類的東西就好
{% endhint %}

{% hint style="info" %}
輸出變數值簡化版

```php
<?=$name?>
```
{% endhint %}

## 

