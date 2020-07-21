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

## 執行SQL指令

* **`$pdo->exec(`**_**`SQL命令`**_**`)`**
  * 用來執行不會取得result set的指令，例如inset、update、delete
* **`$pdo->query(`**_**`SQL命令`**_**`)`**
  * 用來執行會取得result set的指令，例如select
* **`$pdo->prepare(`**_**`SQL命令`**_**`)`**
  * 用來事先編譯好一個SQL敘述

{% tabs %}
{% tab title="exec" %}
* **`$pdo->exec(`**_**`SQL命令`**_**`)`**
  * 用來執行不會取得result set的指令，例如inset、update、delete

```php
<?php 
try {
	$dsn = "mysql:host=localhost;port=3306;dbname=demo;charset=utf8"
	$user = "root";
	$password = "root";
	$options = array(PDO::ATTR_CASE=>PDO::CASE_NATURAL, PDO::ATTR_ERRMODE=>PDO::ERRMODE_EXCEPTION);
	$pdo = new PDO($dsn, $user, $password, $options);
	echo "連線成功~<br>";	

	$sql = "update emp set sal += 1000";//PHP指令
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
  * 用來執行會取得result set的指令，例如select

```php
<?php 
try {
	$dsn = "mysql:host=localhost;port=3306;dbname=books;charset=utf8";
	$user = "root";
	$password = "root";
	$options = array(PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION);
	$pdo = new PDO($dsn, $user, $password, $options);

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
	$dsn = "mysql:host=localhost;port=3306;dbname=books;charset=utf8";
	$user = "root";
	$password = "root";
	$options = array(PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION);
	$pdo = new PDO($dsn, $user, $password, $options);

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
{% endtab %}

{% tab title="👈取得物件的方法fetch" %}
### fetch：回傳一維陣列

```php
<?php 
try {
	$dsn = "mysql:host=localhost;port=3306;dbname=books;charset=utf8";
	$user = "root";
	$password = "root";
	$options = array(PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION);
	$pdo = new PDO($dsn, $user, $password, $options);

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
	$dsn = "mysql:host=localhost;port=3306;dbname=books;charset=utf8";
	$user = "root";
	$password = "root";
	$options = array(PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION);
	$pdo = new PDO($dsn, $user, $password, $options);

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
	$dsn = "mysql:host=localhost;port=3306;dbname=books;charset=utf8";
	$user = "root";
	$password = "root";
	$options = array(PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION);
	$pdo = new PDO($dsn, $user, $password, $options);

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

{% tab title="Second Tab" %}
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
        <tr>
            <th>書號</th>
            <td><?=$findbook["psn"]?></td>
        </tr>
        <tr>
            <th>書名</th>
            <td><?=$findbook["pname"]?></td>
        </tr>
        <tr>
            <th>價格</th>
            <td><?=$findbook["price"]?></td>
        </tr>
        <tr>
            <th>作者</th>
            <td><?=$findbook["author"]?></td>
        </tr>
        <tr>
            <th>頁數</th>
            <td><?=$findbook["pages"]?></td>
        </tr>
        <tr>
            <th>圖檔</th>
            <td><?=$findbook["image"]?></td>
        </tr>
    </table>
</div>
</body>
</html>
```
{% endtab %}
{% endtabs %}

