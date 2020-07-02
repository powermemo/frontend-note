# 資料型別與變數

## 變數

* 語法：`$變數名稱=值;`錢字號開頭。 範例：`$name = 'Sara';`
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

* 「$\_GET\["_欄位名稱_"\]」資料安全
* 「$\_POST\["_欄位名稱"_\]」資料不安全，例如GOOGLE搜尋，網頁欄都看得到。
* 「$\_REQUEST\["_欄位名稱_"\]」可取代「$\_GET...」、「$\_POST...」。

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

//或是使用大括號框住「回傳資料標籤」，就不會受外部引號影響
<?php
        echo "使用者：,{$_GET["memId"]},<br>"
?>
//可使用「$_GET...」、「$_POST...」或是「$_GREQUEST...」
//「$_GREQUEST...」可取代「$_GET...」、「$_POST...」
```

{% hint style="info" %}
若引字號會衝突ex. `"使用者：,$_GET["memId"],<br>";`  
則使用大括號「{}」框住。：`"使用者：,{$_GET["memId"]},<br>";`
{% endhint %}

## 

