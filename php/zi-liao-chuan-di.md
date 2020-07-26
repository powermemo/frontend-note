# 資料傳遞

## 透過表單傳遞資料

傳遞資料的標籤：

* input
* textarea
* select&gt;option 下拉式選單

詳細範例可以參照老師的範例檔：

* prodQuery.html
* prodQuery.php
* prodQueryToDb.php

{% tabs %}
{% tab title="First Tab" %}
#### 查書單書號\(對應範例檔案prodQuery.html\)

```markup
<form method="get" action="08proQuery.php">
    <label for="bookSearch">書籍：</label>
    <input type="text" id="bookSearch" placeholder="請輸入書號" name="pSn">
    <input type="submit" value="查詢">
</form>
```

#### 查詢到的書單明細\(對應範例檔案prodQuery.php\)

```php
<?php
    $psn = $_GET["pSn"];
    $errMsg='';
    try{
        require_once("../connectBooks.php");
        $sql = "SELECT * FROM products WHERE psn = ".$_GET['pSn']." ";
        $searchPro = $pdo->query($sql);
    }catch(PDOException $e){
        $errMsg .= "錯誤：".$e->getMessage()."<br>";
        $errMsg .= "行號：".$e->getLine()."<br>";
    }
?>

```
{% endtab %}

{% tab title="Second Tab" %}

{% endtab %}
{% endtabs %}

## 透過URL傳遞資料



## 透過客戶端cookie傳遞資料



## 透過伺服端session傳遞資料

