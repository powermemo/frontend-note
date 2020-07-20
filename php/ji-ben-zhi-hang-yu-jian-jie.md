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

## 組態檔\(php.ini\)

改變預設值\(例如時區\)的步驟，以下是以「更改為台灣時區」作為範本

{% tabs %}
{% tab title="更改時區" %}
1. 到C槽\(你存放的位置\)php資料夾找到「php.ini-development」檔案，複製一份
2. 將複製的那份檔案，更改副檔名為「php.ini」
3. 修改檔案內容的「**date.timezone=**」，後面加上「Asia/Taipei」 再砍掉前面註解符號「;」

p.s. 若時區無更動，IIS重新整理。

![](../.gitbook/assets/image%20%2816%29.png)
{% endtab %}

{% tab title="短標籤可以作用" %}
1. 到C槽\(你存放的位置\)php資料夾找到「php.ini-development」檔案，複製一份
2. 將複製的那份檔案，更改副檔名為「php.ini」
3. 修改檔案內容的「**short\_open\_tag=On**」
{% endtab %}
{% endtabs %}

## 

