# 存取MySQL資料庫

## 前置作業

以下的mac電腦都可以不用弄\(已經好了\)。

{% hint style="info" %}
【引用PDO指令】\(一種安全性較佳的指令\)

1. 找到ini檔，把以下註解拿掉 extension = mysqli extension = pdo\_mysql
2. 重整IIS
{% endhint %}

{% hint style="info" %}
【使用phpMyAdmin】\(一種網頁版的操作介面\)

1. 下載phpMyAdmin\(老師提供\)，丟到wwwroot資料夾。
2. 到IIS打開phpMyAdmin資料夾的「index.php」檔案。
{% endhint %}

## PDO指令\(常數\)\[官網[連結](https://www.php.net/manual/en/pdo.constants.php)\]

利用「PDO」存取SQL資料，是安全性較佳的方法。  
PDO可連結更多資料庫系統、PDO可避免SQL injection攻擊。

老師提供較常使用的指令：

{% tabs %}
{% tab title="param" %}
**`PDO::PARAM_BOOL`** \([integer](https://www.php.net/manual/en/language.types.integer.php)\)Represents a boolean data type.

**`PDO::PARAM_NULL`** \([integer](https://www.php.net/manual/en/language.types.integer.php)\)Represents the SQL NULL data type.

**`PDO::PARAM_INT`** \([integer](https://www.php.net/manual/en/language.types.integer.php)\)Represents the SQL INTEGER data type.

**`PDO::PARAM_STR`** \([integer](https://www.php.net/manual/en/language.types.integer.php)\)Represents the SQL CHAR, VARCHAR, or other string data type.

**`PDO::PARAM_STR_NATL`** \([integer](https://www.php.net/manual/en/language.types.integer.php)\)Flag to denote a string uses the national character set. Available since PHP 7.2.0

**`PDO::PARAM_STR_CHAR`** \([integer](https://www.php.net/manual/en/language.types.integer.php)\)Flag to denote a string uses the regular character set. Available since PHP 7.2.0

**`PDO::PARAM_LOB`** \([integer](https://www.php.net/manual/en/language.types.integer.php)\)Represents the SQL large object data type.

**`PDO::PARAM_STMT`** \([integer](https://www.php.net/manual/en/language.types.integer.php)\)Represents a recordset type. Not currently supported by any drivers.

**`PDO::PARAM_INPUT_OUTPUT`** \([integer](https://www.php.net/manual/en/language.types.integer.php)\)Specifies that the parameter is an INOUT parameter for a stored procedure. You must bitwise-OR this value with an explicit PDO::PARAM\_\* data type.
{% endtab %}

{% tab title="fetch" %}
**`PDO::FETCH_LAZY`** \([integer](https://www.php.net/manual/en/language.types.integer.php)\)Specifies that the fetch method shall return each row as an object with variable names that correspond to the column names returned in the result set. 

**`PDO::FETCH_LAZY`** creates the object variable names as they are accessed. Not valid inside [PDOStatement::fetchAll\(\)](https://www.php.net/manual/en/pdostatement.fetchall.php).

**`PDO::FETCH_ASSOC`** \([integer](https://www.php.net/manual/en/language.types.integer.php)\)Specifies that the fetch method shall return each row as an array indexed by column name as returned in the corresponding result set. If the result set contains multiple columns with the same name, 

**`PDO::FETCH_ASSOC`** returns only a single value per column name.

**`PDO::FETCH_NAMED`** \([integer](https://www.php.net/manual/en/language.types.integer.php)\)Specifies that the fetch method shall return each row as an array indexed by column name as returned in the corresponding result set. If the result set contains multiple columns with the same name, 

**`PDO::FETCH_NAMED`** returns an array of values per column name.

**`PDO::FETCH_NUM`** \([integer](https://www.php.net/manual/en/language.types.integer.php)\)Specifies that the fetch method shall return each row as an array indexed by column number as returned in the corresponding result set, starting at column 0.

**`PDO::FETCH_BOTH`** \([integer](https://www.php.net/manual/en/language.types.integer.php)\)Specifies that the fetch method shall return each row as an array indexed by both column name and number as returned in the corresponding result set, starting at column 0.
{% endtab %}

{% tab title="others" %}
**`PDO::ERRMODE_SILENT`** \([integer](https://www.php.net/manual/en/language.types.integer.php)\)Do not raise an error or exception if an error occurs. The developer is expected to explicitly check for errors. This is the default mode. See [Errors and error handling](https://www.php.net/manual/en/pdo.error-handling.php) for more information about this attribute.

**`PDO::ERRMODE_WARNING`** \([integer](https://www.php.net/manual/en/language.types.integer.php)\)Issue a PHP **`E_WARNING`** message if an error occurs. See [Errors and error handling](https://www.php.net/manual/en/pdo.error-handling.php) for more information about this attribute.

**`PDO::ERRMODE_EXCEPTION`** \([integer](https://www.php.net/manual/en/language.types.integer.php)\)Throw a [PDOException](https://www.php.net/manual/en/class.pdoexception.php) if an error occurs. See [Errors and error handling](https://www.php.net/manual/en/pdo.error-handling.php) for more information about this attribute.

**`PDO::CASE_NATURAL`** \([integer](https://www.php.net/manual/en/language.types.integer.php)\)Leave column names as returned by the database driver.

**`PDO::CASE_LOWER`** \([integer](https://www.php.net/manual/en/language.types.integer.php)\)Force column names to lower case.

**`PDO::CASE_UPPER`** \([integer](https://www.php.net/manual/en/language.types.integer.php)\)Force column names to upper case.

**`PDO::NULL_NATURAL`** \([integer](https://www.php.net/manual/en/language.types.integer.php)\)

**`PDO::NULL_EMPTY_STRING`** \([integer](https://www.php.net/manual/en/language.types.integer.php)\)
{% endtab %}
{% endtabs %}

## 連結資料庫

{% tabs %}
{% tab title="new PDO建立" %}
* 建立PDO物件：`$pdo = new PDO($dsn , $user, $password, $options);`
  * `$dsn`：資料庫連線資訊
    * `mysql:`：前置詞
    * `host:`：主機
    * `port`：port number
    * `dbname`：資料庫名稱
    * `charset`：字元集
  * `$user`：使用者帳號
  * `$password`：使用者密碼
  * `$options`：描述資料庫連接時的一些資訊； 以關聯性陣列的方式表示。

```php
//分號隔著寫，中間不要空白
$dsn = "mysql:host=localhost;port=3306;dbname=books;charset=urt8";
$user = "使用者帳號";
$password = "使用者密碼";
$pdo = new PDO($dsn , $user, $password);
```

```php
//多了$options
$dsn = "mysql:host=localhost;port=3306;dbname=books;charset=urt8";
$user = "使用者帳號";
$password = "使用者密碼";
$options = array(PDO::ATTR_CASE=>PDO::CASE_NATURAL, PDO::ATTR_ERRMODE=>PDO::ERRMODE_EXCEPTION);
$pdo = new PDO($dsn , $user, $password, $options);
```
{% endtab %}

{% tab title="try..catch錯誤時" %}
設定正常運作時執行指令\(try\)、錯誤時的執行指令\(catch\)

* `PDOException`：例外物件
* `getMessage()`：出了甚麼錯
* `getLine()`：錯在第幾行
* 「...-&gt;...」是類似於JS物件的寫法

```php
try{
    $dsn = 'mysql:host=localhost;port=3306;dbname=demo;charset=utf8';
    $user = 'root';
    $password = 'root';
    // $options = array(2=>0, 8=>2); //這樣陣列記不住所以用下面的
    $options = array(PDO::ATTR_CASE=>PDO::CASE_NATURAL, PDO::ATTR_ERRMODE=>PDO::ERRMODE_EXCEPTION);
    $pdo = new PDO($dsn, $user, $password, $options);
    echo "連線成功<br>";

    $sql = 'update emp set sal += 1000';//字串內是PHP指令
    $affectedHow = $pdo->exec($sql);//使用「$...->exec($字串指令變數)」
    echo '成功了異動',{$affectedHow},'筆資料';
    
}catch(PDOException $e){//🟡例外物件
    echo "錯誤原因：",$e->getMessage(),"<br>";//🟡出了甚麼錯
    echo "錯誤原因：",$e->getLine(),"<br>";//🟡錯在第幾行
}
```
{% endtab %}
{% endtabs %}

### options

{% tabs %}
{% tab title="可設定項目" %}
* `PDO::ATTR_CASE`：大小寫屬性
* `PDO::ATTR_ERRMODE`：錯誤發生時
* `PDO::ATTR_ORACLE_NULLS`：null和空字串轉換
* `PDO::ATTR_AUTOCOMMIT`：是否自動commit\(true\)
* `PDO::MYSQL_ATTR_USE_BUFFERED_QUERY`：
* `PDO::ATTR_DEFAULT_FETCH_MODE`：存取資料模式
{% endtab %}

{% tab title="範例" %}


```php
$options = array(
    PDO::ATTR_CASE=>PDO::CASE_NATURAL,
    PDO::ATTR_ERRMODE=>PDO::ERRMODE_EXCEPTION,
    PDO::ATTR_ORACLE_NULLS=>PDO::NULL_NATURAL);
```
{% endtab %}
{% endtabs %}

### 登入資料庫帳密

小組專題時，大家的資料庫帳密都不大相同。  
假設呈現的PHP檔案是「main.php」，將裡面資料庫登入的程式碼另存新檔 例如「connect.php」  
再將「main.php」連結「connect.php」

{% tabs %}
{% tab title="connect" %}
```php
<?php
$dsn = "mysql:host=localhost;port=3306;dbname=books;charset=utf8";
$user = '使用者名稱';
$password = '使用者密碼';
$options = array(PDO::ATTR_ERRMODE=>PDO::ERRMODE_EXCEPTION);
$pdo = new PDO($dsn, $user, $password, $options);
?>
```
{% endtab %}

{% tab title="main" %}
```php
<?php
require("connectBooks.php");
//像JS的script:src，像CSS的@import，像HTML的link
?>
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
連結資料庫連線的檔案：  
`require_once("引用檔案路徑");  或是  
include_once("引用檔案路徑");`

※ 像JS的script:src，像CSS的@import，像HTML的link
{% endhint %}

## 執行SQL指令

* **`$pdo->exec(`**_**`SQL命令`**_**`)`**
  * 用來執行不會取得result set的指令，例如inset、update、delete（DML）
* **`$pdo->query(`**_**`SQL命令`**_**`)`**
  * 用來執行會取得result set的指令，例如select（DQL）
* **`$pdo->prepare(`**_**`SQL命令`**_**`)`**
  * 用來事先編譯好一個SQL敘述，可以執行inset、update、delete、select等（DQL+DML）
  * 指令內放未知數，編譯它再帶資料進去，防止別人竄改我資料庫\(SQL\)資料。

{% hint style="info" %}
PHP的「-&gt;」相當於JS的「.」  
ex.PHP的「`$pdo->query($sql);`」  
ex.JS的「`xxx.addEventListener('click',function(){});`」
{% endhint %}

{% tabs %}
{% tab title="exec" %}
* **`$pdo->exec(`**_**`SQL命令`**_**`)`**
  * 用來執行不會取得result set的指令，例如**inset、update、delete**

```php
<?php 
try {
	$dsn = "mysql:host=localhost;port=3306;dbname=demo;charset=utf8"
	$user = "root";
	$password = "root";
	$options = array(PDO::ATTR_CASE=>PDO::CASE_NATURAL, PDO::ATTR_ERRMODE=>PDO::ERRMODE_EXCEPTION);
	$pdo = new PDO($dsn, $user, $password, $options);
	echo "連線成功~<br>";	

	$sql = "update emp set sal += 1000";//PHP指令，加薪$1000
	$pdo->exec($sql);//🟡透過PDO執行SQL指令
	echo "異動成功~<br>";	
	
} catch (PDOException $e) {
	echo "錯誤原因 : ", $e->getMessage(), "<br>";
	echo "錯誤行號 : ", $e->getLine(), "<br>";
}
?> 
```
{% endtab %}

{% tab title="query" %}
* **`$pdo->query(`**_**`SQL命令`**_**`)`**
  * 用來執行會取得result set的指令，例如**select**

```php
<?php 
try {
	require("connectBooks.php");//這個範例應該要連郭老師資料庫的，連books是錯誤的..
	$sql = "select * from products";//🟡
	$products = $pdo->query($sql);//🟡
	
} catch (PDOException $e) {
	echo "錯誤原因 : ", $e->getMessage(), "<br>";
	echo "錯誤行號 : ", $e->getLine(), "<br>";
}
?>    
```

### 取回result set的方法

```php
<?php 
try {
	require("connectBooks.php");//這個範例應該要連郭老師資料庫的，連books是錯誤的..
	$sql = "select * from products";
	$products = $pdo->query($sql);
	
	echo "<table align='center'>";
	echo "<tr><th>書號</th><th>書名</th><th>價格</th><th>作者</th></tr>";
	while( $prodRow = $products->fetch(PDO::FETCH_ASSOC)){//🟡fetch一維陣列
	//當抓得到一筆資料
	?>
		<tr>
		<td><?=$prodRow["psn"]?></td>//🟡中括號內是資料庫表格表頭名稱
		<td><?=$prodRow["pname"]?></td>//🟡
		<td><?=$prodRow["price"]?></td>//🟡
		<td><?=$prodRow["author"]?></td>//🟡
		</tr>
	<?php
	}
	echo "</table>";
} catch (PDOException $e) {
	echo "錯誤原因 : ", $e->getMessage(), "<br>";
	echo "錯誤行號 : ", $e->getLine(), "<br>";
	
}

?>    
```
{% endtab %}

{% tab title="👈取得物件的方法fetch¿\(\)👉" %}
### fetch：回傳一維陣列

```php
<?php 
try {
	$require("connectBooks.php");
	$sql = "select * from products";
	$products = $pdo->query($sql);
	echo "<table align='center'>";
	echo "<tr><th>書號</th><th>書名</th><th>價格</th><th>作者</th></tr>";
	while( $prodRow = $products->fetch(PDO::FETCH_ASSOC)){//🟡fetch
	//當抓得到一筆資料
	?>
		<tr>
		<td><?=$prodRow["psn"]?></td>//🟡
		<td><?=$prodRow["pname"]?></td>//🟡
		<td><?=$prodRow["price"]?></td>//🟡
		<td><?=$prodRow["author"]?></td>//🟡
		</tr>
	<?php
	}

	echo "</table>";
} catch (PDOException $e) {
	echo "錯誤原因 : ", $e->getMessage(), "<br>";
	echo "錯誤行號 : ", $e->getLine(), "<br>";
	
}

?>    
```

### fetchAll：回傳二維陣列

```php
<?php 
try {
	require("connectBooks.php");
	$sql = "select * from `member`";
	$products = $pdo->query($sql);//🟡
	$prodRows = $products->fetchAll(PDO::FETCH_ASSOC);//🟡
} catch (PDOException $e) {
	echo "錯誤原因 : ", $e->getMessage(), "<br>";
	echo "錯誤行號 : ", $e->getLine(), "<br>";
}
?>
//👆寫在<head>之上
//👇寫在<body>裡面


<table align='center'>
<tr><th>編號</th><th>姓名</th><th>ID</th><th>密碼</th><th>信箱</th><th>性別</th><th>生日</th><th>電話</th></tr>
<?php
foreach($prodRows as $i=>$prodRow){//🟡
?>
	<tr>
	<td><?=$prodRow["no"]?></td>
	<td><?=$prodRow["memName"]?></td>
	<td><?=$prodRow["memId"]?></td>
	<td><?=$prodRow["memPsw"]?></td>
	<td><?=$prodRow["email"]?></td>
	<td><?=$prodRow["sex"]?></td>
	<td><?=$prodRow["birthday"]?></td>
	<td><?=$prodRow["tel"]?></td>
	</tr>
<?php
}
?>
</table> 
```

### fetchObject：回傳一個物件

```php
<?php 
try {
	require("connectBooks.php");
	$sql = "select * from products";
	$products = $pdo->query($sql);
} catch (PDOException $e) {
	echo "錯誤原因 : ", $e->getMessage(), "<br>";
	echo "錯誤行號 : ", $e->getLine(), "<br>";
}
?>

//👆寫在<head>之上
//👇寫在<body>裡面

<table align='center'>
<tr><th>書號</th><th>書名</th><th>價格</th><th>作者</th></tr>
<?php//🟡
while( $prodRow = $products->fetchObject()){//當抓得到一筆資料, 取回來以物件的形式
?>
	<tr>
	<td><?=$prodRow->psn?></td>//🟡
	<td><?=$prodRow->pname?></td>//🟡
	<td><?=$prodRow->price?></td>//🟡
	<td><?=$prodRow->author?></td>//🟡
	</tr>
<?php
}
?>
</table> 
```
{% endtab %}

{% tab title="prepare" %}
* **`$pdo->prepare(`**_**`SQL命令`**_**`)`**
  * 可以執行**inset、update、delete、select**
  * 用來事先編譯好一個SQL敘述
  * 為什麼要用prepare？ 當指令內含有**未知數**，如前端表格送的資料， 我在我的指令內放未知數，編譯它再帶資料進去 防止別人竄改我資料庫\(SQL\)資料。

```php
<?php
$errMsg = "";
try{
    require_once("../connectBooks.php");//如果require在迴圈裡就拉不出來，所以用require_once
    //===================================================方法一：question parameter
    $sql = "select * from `member` where memId=? and memPsw=?";//🟡「?」
    $member = $pdo->prepare($sql);//🟣將prepare($sql)編譯執行
    $member->binValue(1, $_GET['memId']);//🟡1代表第一個問號，要帶甚麼值進去(前端送來的資料)。
    $member->binValue(2, $_GET['memPsw']);//🟡2代表第二個問號，要帶甚麼值進去(前端送來的資料)。
    $member->execute();//🟣執行


    //===================================================方法二：named parameter
    //我不要第一個第二個問號，我會記不住，所以我用以下的指令
    $sql = "select * from `member` where memId=:aaa and memPsw=:bbb";//🟡「:自定義參數名」
    $member = $pdo->prepare($sql);//🟣
    $member->binValue(':aaa', $_GET['memId']);//🟡:aaa，要帶甚麼值進去(前端送來的資料)。
    $member->binValue(':bbb', $_GET['memPsw']);//🟡:bbb，要帶甚麼值進去(前端送來的資料)。
    $member->execute();//🟣執行
  }catch(PDOException $e){
    $errMsg .= "錯誤原因：".$e -> getMessage(). "<br>";
    $errMsg .= "錯誤行號 : ".$e -> getLine(). "<br>";
  }
?>
```

```php
//下面函式不動
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>login</title>
</head>
<body>
<?php
if($errMsg != ""){
    echo "<div>$errMsg</div>";
}elseif($member->rowCount() ==0){//一筆都沒找到
    echo "<center>帳密錯誤</center>";
}else{                            //取回登入者的資訊
    $memRow = $member->fetch(PDO::FETCH_ASSOC);
    echo  $memRow["memName"], ",您好！</br>";
}
?>
</body>
</html>
```
{% endtab %}

{% tab title="👈引數提供bind¿\(\)" %}
#### bindValue\(\)

第二個參數可以是變數、可以是字面值（如下例10）

```php
//=====bindValue()---問號
$sql = "update products set price=price-?";//先用?(尚未帶值進去)
$statement = $pdo->prepare($sql);
$statement->bindValue(1,10);//🟡1表示第一個問號，要填甚麼進去(10)
$statement->execute();


//=====bindValue()---:參數
$sql = "update products set price=price-:amount";//:amount自定義參數名
$statement = $pdo->prepare($sql);
$statement->bindValue(:amount,10);//🟡參數:amount，要填甚麼進去(10)
$statement->execute();
```

#### bindParam\(\)

第二個參數只能是變數（如下例$amount）

```php
//=====bindParam()---問號
$sql = "update products set price=price-?";//先用?(尚未帶值進去)
$statement = $pdo->prepare($sql);
$statement->bindParam(1,10);//🚫錯誤，第二個引數不能是字面表示法
$statement->execute();


//=====bindValue()---:參數
$sql = "update products set price=price-:amount";//:amount自定義參數名
$statement = $pdo->prepare($sql);
$statement->bindParam(:amount,$amount);//🟡參數:amount，要填甚麼進去($amount)
$statement->execute();
```

#### bindColumn\(\)

```php
$sql = "select * from products where price<500";
$products = $pdo->query($sql);
$products->bindColumn(1,$psn);    //第一直欄
$products->bindColumn(2,$pname);    //第二直欄
$products->bindColumn(3,$price);    //第三直欄
$products->bindColumn(4,$author);    //第四直欄
$products->fetch();
```
{% endtab %}
{% endtabs %}

## 🍵作業－會員名單、查詢書籍

{% tabs %}
{% tab title="會員名單" %}
.

```php
<?php
try{
    $dsn = "mysql:host=localhost;port=3306;dbname=books;charset=utf8";
    $user = '使用者名稱';
    $password = '使用者密碼';
    $opsitions = array(PDO::ATTR_ERRMODE=>PDO::ERRMODE_EXCEPTION);
    $pdo = new PDO($dsn, $user, $password, $opsitions);
    $sql = 'select * from `member`';
    $members = $pdo->query($sql);
}catch(PDOException $e){
    echo '錯誤原因：',$e->getMessage(),'<br>';
    echo '錯誤行號：',$e->getLine(),'<br>';
}
?>

<!DOCTYPE html>
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>7-PHP 資料庫會員名單</title>
    <style>
    body{
        font-family:arial,微軟正黑體;
    }
    table{
        margin:auto;
    }
    table,th,td{
        border:1px solid black;
        border-collapse: collapse;
    }
    th{
        background-color:pink;
    }
    </style>
</head>
<body>
    <table>
        <tr>
            <th>編號</th>
            <th>姓名</th>
            <th>帳號</th>
            <th>密碼</th>
            <th>email</th>
            <th>性別</th>
            <th>生日</th>
            <th>電話</th>
        </tr>
        <?php
        while( $someone = $members->fetch(PDO::FETCH_ASSOC)){//當抓得到一筆資料
        ?>
        <tr>
            <td><?=$someone["no"]?></td>
            <td><?=$someone["memName"]?></td>
            <td><?=$someone["memId"]?></td>
            <td><?=$someone["memPsw"]?></td>
            <td><?=$someone["email"]?></td>
            <td><?=$someone["sex"]?></td>
            <td><?=$someone["birthday"]?></td>
            <td><?=$someone["tel"]?></td>
        </tr>
        <?php
        }
        ?>
    </table>
</body>
</html>
```
{% endtab %}

{% tab title="書單" %}
.

```markup
<!--HTML-->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        body{
            font-family: arial,微軟正黑體;
        }
    </style>
</head>
<body>
    <p>書籍只有7本，請不要亂來😏</p>
    <form method="get" action="08proQuery.php">
        <label for="bookSearch">書籍：</label>
        <input type="text" id="bookSearch" placeholder="請輸入書籍之書號" name="pSn">
        <input type="submit" value="查詢">
    </form>
</body>
</html>
```

```php
//PHP
<?php
    try{
        $dsn = 'mysql:host=localhost;port=3306;dbname=books;charset=utf8';
        $user = '使用者名稱';
        $password = '使用者密碼';
        $options = array(PDO::ATTR_ERRMODE=>PDO::ERRMODE_EXCEPTION);
        $pdo = new PDO($dsn, $user, $password, $options);
        $sql = "SELECT * FROM products WHERE psn = ".$_GET['pSn']." ";//🟡
        $searchPro = $pdo->query($sql);
    }catch(PDOException $e){
        echo 'FIND ERROR:',$e->getMessage(),'<br>';
        echo 'LINE:',$e->getLine(),'<br>';
    }
    //http://vvv.lionfree.net/learnshow.php?l_url=html_037.html
?>
<!DOCTYPE html>
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>8-PHP搜尋書單</title>
    <style>
    body{
        font-family:arial,微軟正黑體;
    }
    h1,p{
        text-align:center;
    }
    table{
        margin:auto;
    }
    table,th,td{
        border:1px solid black;
        border-collapse: collapse;
    }
    th{
        background-color:pink;
    }
    </style>
</head>
<body>
<div class="wrap">
    <h1>書籍基本資料</h1>
    <table>
    <?php
    $findbook = $searchPro->fetch(PDO::FETCH_ASSOC);
    ?>
        <tr><th>書號</th><td><?=$findbook["psn"]?></td></tr>
        <tr><th>書名</th><td><?=$findbook["pname"]?></td></tr>
        <tr><th>價格</th><td><?=$findbook["price"]?></td></tr>
        <tr><th>作者</th><td><?=$findbook["author"]?></td></tr>
        <tr><th>頁數</th><td><?=$findbook["pages"]?></td></tr>
        <tr><th>圖檔</th><td><?=$findbook["image"]?></td></tr>
    </table>
</div>
</body>
</html>
```
{% endtab %}

{% tab title="書單-老師的PHP" %}
.

```php
<?php

$psn = $_REQUEST["psn"];
$errMsg = "";//🟡
//連線資料庫
try{
  require_once("../connectBooks.php");//🔰

  $sql = "select * from products where psn = $psn";
  $products = $pdo->query($sql);
}catch(PDOException $e){
  $errMsg .= "錯誤原因 : ".$e -> getMessage(). "<br>";//🟡
  $errMsg .= "錯誤行號 : ".$e -> getLine(). "<br>";//🟡
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
  <!-- 🟡🟡以下為查不到資料時的碼🟡🟡 -->
<?php 
if( $errMsg != ""){ //例外
  echo "<div><center>$errMsg</center></div>";
}elseif($products->rowCount()==0){
      echo "<div><center>查無此商品資料</center></div>"; 
  // 🟡🟡以上為查不到資料時的碼🟡🟡 
}else{
      $prodRow = $products->fetchObject();
?>
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
</body>
</html>

```
{% endtab %}
{% endtabs %}

### 



