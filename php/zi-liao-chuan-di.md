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

```php
<?php
$errMsg = '';
try{
    require_once('../connectBooks.php');
    $sql = "update products set pname=:pname,
                                price=:price,
                                author=:author,
                                pages=:pages,
                                image=:image   where psn=:psn";
    $products = $pdo->prepare($sql);
    $products->bindValue(':psn',$_GET['psn']);
    $products->bindValue(':pname',$_GET['pname']);
    $products->bindValue(':price',$_GET['price']);
    $products->bindValue(':author',$_GET['author']);
    $products->bindValue(':pages',$_GET['pages']);
    $products->bindValue(':image',$_GET['image']);
    $products->execute();
}catch(PDOException $e){
    $errMsg .= "錯誤原因 : ".$e -> getMessage(). "<br>";
    $errMsg .= "錯誤行號 : ".$e -> getLine(). "<br>";
}
?>
//👆頁面最上方
//👇body裡面
<?php
if($errMsg != ""){
    echo "<center>$errMsg</center>";
}else{
    echo "異動成功~<br>";
}

?>
```
{% endtab %}

{% tab title="Second Tab" %}

{% endtab %}
{% endtabs %}

## 透過URL傳遞資料

用a連結去抓資料

{% tabs %}
{% tab title="產品清單範例" %}
#### 對應範例檔案prodList.php

```php
while($prodRow = $products->fetch(PDO::FETCH_ASSOC)){
    <a href="prodQuery.php?psn=<?=$prodRow['psn']?>"></a>
}
```

#### 對應範例檔案prodQuery.php
{% endtab %}
{% endtabs %}



## 透過客戶端cookie傳遞資料

寫入語法：`setcookie("自定義cookie名稱", "cookie的值" [, 時間]);`

* cookie名稱：自定義，例如`memId`。
* 值：cookie的值，例如`$_GET["memId"`\]。
* 時間：選填，cookie保留的期限，在設定時間內有效，例如`time()+60`； 若未設定時間，關閉瀏覽器時即刻刪除cookie。

讀出語法：`$_COOKIE["自定義cookie名稱"];`，例如`$_COOKIE["memId"];`。

{% tabs %}
{% tab title="登入案例" %}
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
	$member = $pdo->prepare( $sql ); 			//先編譯好
	$member->bindValue(":memId", $memId); //代入資料
	$member->bindValue(":memPsw", $memPsw);
	$member->execute();//執行之

	if( $member->rowCount() == 0 ){				//找不到時怎麼做
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

#### 登入成功的會員專區 \(對應範例檔案cookieMember.php\)

```php
<?php
echo "帳號 : ", $_COOKIE["memId"],"<br>";
echo "姓名 : ", $_COOKIE["memName"],"<br>";
echo "email : ", $_COOKIE["email"],"<br>";
?> 
```
{% endtab %}
{% endtabs %}

## 透過伺服端session傳遞資料

