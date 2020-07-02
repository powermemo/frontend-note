# 基本執行與簡介

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

## 變數

* 語法：`$變數名稱=值;` 範例：`$name = 'Sara';`
* 大小寫視為不同
* 不須事先宣告

{% hint style="info" %}
其他「命名規則」、「資料型態」等等跟JS很像，就不另外寫了。
{% endhint %}

## 字串

{% tabs %}
{% tab title="單引號" %}
使用方法較有限  
使用「\」斜線跳脫字元

```php
<?php
        echo 'I am Sara','<br>';
        echo 'I am "Sara"', '<br>';
        echo 'I am \'Sara\'', '<br>';
        echo 'I am \\Sara\\', '<br>';
?>
```

呈現結果

I am Sara  
I am "Sara"  
I am 'Sara'  
I am \Sara\
{% endtab %}

{% tab title="雙引號" %}
提供較多的跳脫字元

| 跳脫字元 | 說明 |
| :--- | :--- |
| \n | HTML原始碼換行 |
| \r | ENTER鍵 |
| \t | TAB鍵 |
| \\ | 反斜線符號 |
| \$ | 「$」符號 |
| \" | 「"」雙引號 |

```php
<?php
        echo "I am Sara",'<br>';
        echo "I am \"Sara\"", '<br>';
        echo "I am 'Sara'", '<br>';
        echo "I am \\Sara\\", '<br>';
?>
```

呈現結果

I am Sara  
I am "Sara"  
I am 'Sara'  
I am \Sara\

```php
<?php
        $name = 'Sara';
        $coco = 70;
        echo '姓名：',$name,'<br>';
        echo "姓名：$name<br>";
        echo "存款：$coco 元<br>";//元前面有加空白
        echo "存款：{$coco}元<br>";//把變數用「大括弧」框起來
        echo "存款：{$coco}*10元<br>";//運算式不可以
?>
```

呈現結果

姓名：Sara  
姓名：Sara  
存款：70 元  
存款：70元  
存款：70\*10元
{% endtab %}
{% endtabs %}

## $\_SERVER變數

```php
<?php
    $_SERVER['REMOTE_ADDR'];//客戶端ip位置
    $_SERVER['PHP_SELF'];//目前檔案路徑及名稱
    $_SERVER['SERVER_NAME'];//伺服器名稱
    phpinfo();//本機端PHP詳細資訊
?>
```

```php
<?php
        echo '您的IP：', $_SERVER["REMOTE_ADDR"],'<br>';//本機端localhost
        if($_SERVER["REMOTE_ADDR"] == "10.120.37.66"){
            echo 'ruru';
        }else{
            echo 'haha';
        }
        echo '目前程式：',$_SERVER["PHP_SELF"],"<br>";
        phpinfo();//本機端PHP詳細資訊
?>
```

## 表單欄位變數取得

▼HTML

```markup
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>表單</title>
</head>
<body>
    <form method="get" action="form.php">
        <div>
            <label for="memId">帳號：</label>
            <input type="text" name="memId" required="required"><br>
        </div>
        <div>
            <label for="memPsw">密碼：</label>
            <input type="password" name="memPsw" required="required">
        </div>
        <input type="submit" value="送出">

    </form>
</body>
</html>
```

▼PHP

```php
<?php
        echo '使用者：',$_GET['memId'],'<br>';//中括號，引號內是標籤的「name」名稱
        echo '密碼：',$_GET['memPsw'],'<br>';//中括號，引號內是標籤的「name」名稱
    ?>
```

