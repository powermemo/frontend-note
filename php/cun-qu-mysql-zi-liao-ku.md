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

```php
try{
    $dsn = 'mysql:host=localhost;port=3306;dbname=demo;charset=utf8';//分號隔著寫，中間不要空白
    $user = 'root';
    $password = 'root';
    // $options = array(2=>0, 8=>2); //這樣陣列記不住所以用下面的
    $options = array(PDO::ATTR_CASE=>PDO::CASE_NATURAL, PDO::ATTR_ERRMODE=>PDO::ERRMODE_EXCEPTION);
    $pdo = new PDO($dsn, $user, $password, $options);
    echo "連線成功<br>";

    $sql = 'update emp set sal += 1000';//字串內是PHP指令
    $affectedHow = $pdo->exec($sql);//使用「$...->exec($字串指令變數)」
    echo '成功了異動',{$affectedHow},'筆資料';
}catch(PDOException $e){
    echo "錯誤原因：",$e->getMessage(),"<br>";
    echo "錯誤原因：",$e->getLine(),"<br>";
}
```
{% endtab %}
{% endtabs %}



