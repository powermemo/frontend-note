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
#### 查書單書號 \(對應範例檔案prodQuery.html\)

```markup
<form method="get" action="08proQuery.php">
    <label for="bookSearch">書籍：</label>
    <input type="text" id="bookSearch" placeholder="請輸入書號" name="pSn">
    <input type="submit" value="查詢">
</form>
```

#### 查詢到的書單明細-可以更動內容 \(對應範例檔案prodQuery.php\)

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

#### 更動內容是否成功 \(對應範例檔案prodQueryToDb.php\)

```text

```
{% endtab %}

{% tab title="Second Tab" %}

{% endtab %}
{% endtabs %}

## 透過URL傳遞資料

{% tabs %}
{% tab title="First Tab" %}

{% endtab %}

{% tab title="Second Tab" %}

{% endtab %}
{% endtabs %}

## 透過客戶端cookie傳遞資料

語法：`setcookie("自定義cookie名稱", "cookie的值" [, 時間]);`

* cookie名稱：自定義，例如`memId`。
* 值：cookie的值，例如`$_GET["memId"`\]。
* 時間：選填，cookie保留的期限，在設定時間內有效 若未設定時間，關閉瀏覽器時即刻刪除cookie。

{% tabs %}
{% tab title="登入案例" %}
已登入介面為例

#### 登入介面 \(對應範例檔案cookieLogin.html\)

```markup
<div id="loginBox">
<form action="cookieLogin.php" method="post">
<p>帳號: <input type="text" name="memId"></p>
<p>密碼: <input type="password" name="memPsw"></p>
<p><input type="submit" value="登入"></p>
</form>
```

#### 登入結果-是否登入成功 \(對應範例檔案cookieLogin.php\)

```php
<?php
$memId = $_POST["memId"];
$memPsw = $_POST["memPsw"];
$errMsg = "";
try {
	require_once("./connectBooks.php");
	$sql = "select * from member` where memId=:memId and memPsw=:memPsw"; 
	$member = $pdo->prepare( $sql ); //先編譯好
	$member->bindValue(":memId", $memId); //代入資料
	$member->bindValue(":memPsw", $memPsw);
	$member->execute();//執行之

	if( $member->rowCount() == 0 ){//找不到時怎麼做
		$errMsg .= "帳密錯誤, <a href='cookieLogin.html'>重新登入</a><br>";
	}else{
		$memRow = $member->fetch(PDO::FETCH_ASSOC);
		//登入成功,將登入者的資料寫入cookie
		setcookie("memId",$memRow["memId"],time()+60);
		setcookie("memName",$memRow["memName"],time()+60);
		setcookie("email",$memRow["email"],time()+60);//一分鐘後失效
		//有效期限若為三天內：time()+3*24*60*60

	}
} catch (PDOException $e) {
	$errMsg .= "錯誤 : ".$e -> getMessage()."<br>";
	$errMsg .= "行號 : ".$e -> getLine()."<br>";
}
?>  
//👆整個網頁最上方
//👇body內
<?php 
if($errMsg !=""){
    echo $errMsg;
}else{
    echo $memRow["memName"], " 您好~<br>";
}

?>

<a href="cookieMember.php">前往會員專區</a>  
```
{% endtab %}
{% endtabs %}

## 透過伺服端session傳遞資料

