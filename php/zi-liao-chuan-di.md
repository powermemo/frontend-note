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
{% tab title="html查資料" %}
#### 查書單書號 \(對應範例檔案prodQuery.html\)

```markup
<form method="get" action="08proQuery.php">
    <label for="bookSearch">書籍：</label>
    <input type="text" id="bookSearch" placeholder="請輸入書號" name="pSn">
    <input type="submit" value="查詢">
</form>
```
{% endtab %}

{% tab title="PHP查到的書單可以異動" %}
#### 查詢到的書單明細-可以更動內容 \(對應範例檔案prodQuery.php\)

```php
<?php
$psn = $_REQUEST["psn"];
$errMsg = "";
//連線資料庫
try{
  require_once("../connectBooks.php");
  $sql = "select * from products where psn = :psn";
  $products = $pdo->prepare($sql);
  $products->bindValue(":psn", $psn);
  $products->execute();
}catch(PDOException $e){
  $errMsg .= "錯誤原因 : ".$e -> getMessage(). "<br>";
  $errMsg .= "錯誤行號 : ".$e -> getLine(). "<br>";
}
?>  
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8" />
<title>查詢商品資料</title>
<style>
th {
  background:#bfbfef;
}
td {
  border-bottom:1px deeppink dotted;
}
</style>
</head>

<body>
<?php 
if( $errMsg != ""){ //例外
  echo "<div><center>$errMsg</center></div>";
}elseif($products->rowCount()==0){
      echo "<div><center>查無此商品資料</center></div>";
}else{
      $prodRow = $products->fetchObject();
?>
<br>
<h2 style="text-align:center;color:deeppink">書籍基本資料</h2>
<form action="prodUpdateToDb.php">
  <input type="hidden" name="psn" value="<?=$prodRow->psn?>">
  <table align="center" width="300" >
    <tr><th>書號</th><td><?=$prodRow->psn?></td></tr>
    <tr><th>書號</th><td><input type="text" name="psn" value="<?=$prodRow->psn?>"disabled></td></tr>
    <tr><th>書名</th><td><input type="text" name="pname"value="<?=$prodRow->pname?>"></td></tr>
    <tr><th>價格</th><td><input type="text" name="price"value="<?=$prodRow->price?>"></td></tr>
    <tr><th>作者</th><td><input type="text" name="author"value="<?=$prodRow->author?>"></td></tr>
    <tr><th>頁數</th><td><input type="text" name="pages"value="<?=$prodRow->pages?>"></td></tr>
    <tr><th>圖檔</th><td><input type="text" name="image"value="<?=$prodRow->image?>"></td></tr>
    <tr><td colspan="2" align="center"><input type="submit" value="確定修改"></td></tr>
  </table>
</form>
  <?php

}
?>
</body>
</html>

```
{% endtab %}

{% tab title="異動是否成功" %}
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
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
<?php
if($errMsg != ""){
    echo "<center>$errMsg</center>";
}else{
    echo "異動成功~<br>";
}

?>
</body>
</html>
```
{% endtab %}
{% endtabs %}

## 透過URL傳遞資料

用a連結去抓資料

{% tabs %}
{% tab title="產品清單範例" %}
#### 書單-附連結 \(對應範例檔案prodList.php\)

```php
<?php 
try {
	require_once("../connectBooks.php");
	$sql = "select * from products";
	$products = $pdo->query($sql);
} catch (PDOException $e) {
	echo "錯誤原因 : ", $e->getMessage(), "<br>";
	echo "錯誤行號 : ", $e->getLine(), "<br>";
}
?>
//👆開頭
//👇body內
<table align='center'>
<tr bgcolor="#bfbfef"><th>書號</th><th>書名</th><th>價格</th><th>作者</th></tr>
<?php
while( $prodRow = $products->fetch(PDO::FETCH_ASSOC)){//當抓得到一筆資料, 取回來以陣列的形式
?>
	<tr>
	<td><?=$prodRow["psn"]?></td>
	<td><a href="prodQuery.php?psn=<?=$prodRow['psn']?>"><?=$prodRow["pname"]?></a></td>
	<td><?=$prodRow["price"]?></td>
	<td><?=$prodRow["author"]?></td>
	</tr>
<?php
}
?>
</table> 
```

#### 書單詳細內容 \(對應範例檔案prodQuery.php\)

```php
<?php
$psn = $_REQUEST["psn"];
$errMsg = "";
//連線資料庫
try{
  require_once("../connectBooks.php");
  $sql = "select * from products where psn = $psn";
  $products = $pdo->query($sql);
}catch(PDOException $e){
  $errMsg .= "錯誤原因 : ".$e -> getMessage(). "<br>";
  $errMsg .= "錯誤行號 : ".$e -> getLine(). "<br>";
}
?>
//👆開頭
//👇body內
<?php 
if( $errMsg != ""){ //例外
  echo "<div><center>$errMsg</center></div>";
}elseif($products->rowCount()==0){
      echo "<div><center>查無此商品資料</center></div>";
}else{
      $prodRow = $products->fetchObject();
?>
  <!-- 🟡🟡🟡🟡🟡 -->
<br>
<h2 style="text-align:center;color:deeppink">書籍基本資料</h2>
  <table align="center" width="300" >
    <tr><th>書號</th><td><?php echo $prodRow->psn;?></td></tr>
    <tr><th>書名</th><td><?php echo $prodRow->pname;?></td></tr>
    <tr><th>價格</th><td><?php echo $prodRow->price;?></td></tr>
    <tr><th>作者</th><td><?php echo $prodRow->author;?></td></tr>
    <tr><th>頁數</th><td><?php echo $prodRow->pages;?></td></tr>
    <tr><th>圖檔</th><td><?php echo $prodRow->image;?></td></tr>
  </table>
  <?php
}
?>
```
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

### 前置作業

1. 在C槽PHP資料夾內，新建資料夾「tmp」
2. php.ini檔，找到「session.save\_path」，將註解「;」拿掉 並修改後方路徑，例如「C:\php-7.4.7\tmp」
3. 重啟IIS

{% tabs %}
{% tab title="First Tab" %}
#### 登入畫面-沒有改 \(對應範例檔案sessionLogin.html\)

```markup
<div id="loginBox">
<form action="sessionLogin.php" method="post">
<p>帳號: <input type="text" name="memId"></p>
<p>密碼: <input type="password" name="memPsw"></p>
<p><input type="submit" value="登入"></p>
</form>
</div>
```

#### 登入結果 \(對應範例檔案sessionLogin.php\)

```php
<?php
$memId = $_POST["memId"];
$memPsw = $_POST["memPsw"];
$errMsg = "";
try {
    require_once("../connectBooks.php");
    $sql = "select * from `member` where memId=:memId and memPsw=:memPsw"; //''
    $member = $pdo->prepare( $sql ); //先編譯好
    $member->bindValue(":memId", $memId); //代入資料
    $member->bindValue(":memPsw", $memPsw);
    $member->execute();//執行之
    if( $member->rowCount() == 0 ){//找不到
        $errMsg .= "帳密錯誤, <a href='sessionLogin.html'>重新登入</a><br>";
    }else{
        $memRow = $member->fetch(PDO::FETCH_ASSOC);
        //登入成功,將登入者的資料寫入session
        session_start();                            //🟡
        $_SESSION["memId"] = $memRow["memId"];      //🟡
        $_SESSION["memName"] = $memRow["memName"];  //🟡
        $_SESSION["no"] = $memRow["no"];            //🟡
        $_SESSION["email"] = $memRow["email"];      //🟡
        $_SESSION["tel"] = $memRow["tel"];          //🟡
    }
} catch (PDOException $e) {
    $errMsg .= "錯誤 : ".$e -> getMessage()."<br>";
    $errMsg .= "行號 : ".$e -> getLine()."<br>";
}
?>
//👆頁面最上方
//👇body內
<?php 
if($errMsg !=""){
    echo $errMsg;
}else{
    echo $memRow["memName"], " 您好~<br>";
}
?>
<a href="sessionMember.php">前往會員專區</a>  
```

#### 前往會員中心-會員資料 \(對應範例檔案\)

```php
<?php
//記得要使用session之前，要先啟用serssion
session_start();
?>
<?php
echo "id : ", session_id() ,"<br>";
//自session中取回登入者資料
echo "帳號 : ", $_SESSION["memId"],  "<br>";
echo "姓名 : ", $_SESSION["memName"], "<br>";  
echo "id : ", $_SESSION["no"], "<br>";
echo "email : ", $_SESSION["email"], "<br>";
echo "tel : ", $_SESSION["tel"], "<br>";
?> 
```
{% endtab %}
{% endtabs %}

