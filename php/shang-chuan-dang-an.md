# 上傳檔案

Client端上傳資料到Server端暫存區檔案會不見，  
所以需要用「copy\(\)」函式將暫存檔儲存於指定路徑。

## Client端上傳檔案注意事項

* 使用「input type="file"」選擇檔案
* 表單以「POST」方法上傳
* form屬性「enctype」為「enctype="mltipart/form-data"」
* 例子

```markup
<form method="post" action="fileUpload.php" enctype="multipart/form-data">
    上傳檔案：<input type="file" name="上傳檔案欄位"> <br>
    <input type="submit" value="送出">
</form>
```

## Server端取得上傳檔案

### php.ini相關設定

* 允許上傳：file\_uploads = on
* 上傳暫存區：upload\_tmp\_dir = C:\php位置....\tmp
* 上傳容量上限：upload\_max\_filesize = 2M

### $\_FILES\[\]取得上傳資料

跟$\_POST\[""\]頗像

* 檔案名稱：`$_FILES["`_`上傳檔案欄位`_`"]["name"]`
* 暫存檔名和路徑：`$_FILES["`_`上傳檔案欄位`_`"]["tmp_name"]`
* 檔案尺寸：`$_FILES["`_`上傳檔案欄位`_`"]["size"]`
* 檔案種類：`$_FILES["`_`上傳檔案欄位`_`"]["type"]`
* 上傳檔案時發生的錯誤代碼：`$_FILES["`_`上傳檔案欄位`_`"]["error"]`。

### $\_FILES\["上傳檔案欄位"\]\["error"\]錯誤代碼

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x4EE3;&#x865F;</th>
      <th style="text-align:left">&#x4EE3;&#x78BC;</th>
      <th style="text-align:left">&#x610F;&#x601D;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0</td>
      <td style="text-align:left">UPLOAD_ERR_OK</td>
      <td style="text-align:left">&#x4E0A;&#x50B3;&#x6210;&#x529F;</td>
    </tr>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">UPLOAD_ERR_INI_SIZE</td>
      <td style="text-align:left">&#x6A94;&#x6848;&#x5927;&#x5C0F;&#x8D85;&#x904E;&#x7CFB;&#x7D71;&#x4E0A;&#x9650;</td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">UPLOAD_ERR_FORM_SIZE</td>
      <td style="text-align:left">&#x6A94;&#x6848;&#x5927;&#x5C0F;&#x8D85;&#x904E;&#x8868;&#x55AE;&#x6307;&#x5B9A;&#x4E0A;&#x9650;(&#x2266;&#x7CFB;&#x7D71;&#x4E0A;&#x9650;)</td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">UPLOAD_ERR_PARTIAL</td>
      <td style="text-align:left">&#x6A94;&#x6848;&#x4E0A;&#x50B3;&#x4E0D;&#x5B8C;&#x6574;</td>
    </tr>
    <tr>
      <td style="text-align:left">4</td>
      <td style="text-align:left">UPLOAD_ERR_NO_FILE</td>
      <td style="text-align:left">&#x672A;&#x6307;&#x5B9A;&#x4E0A;&#x50B3;&#x7684;&#x6A94;&#x6848;</td>
    </tr>
    <tr>
      <td style="text-align:left">6</td>
      <td style="text-align:left">UPLOAD_ERR_NO_TMP_DIR</td>
      <td style="text-align:left">
        <p>&#x672A;&#x5B9A;&#x7FA9;&#x66AB;&#x5B58;&#x5340;&#x6240;&#x4F7F;&#x7528;&#x7684;&#x8CC7;&#x6599;&#x593E;</p>
        <p>//&#x7DB2;&#x9801;&#x958B;&#x767C;&#x7AEF;&#x7684;&#x554F;&#x984C;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">7</td>
      <td style="text-align:left">UPLOAD_ERR_CANT_WRITE</td>
      <td style="text-align:left">&#x7121;&#x6CD5;&#x5BEB;&#x5165;&#x66AB;&#x5B58;&#x5340;</td>
    </tr>
    <tr>
      <td style="text-align:left">8</td>
      <td style="text-align:left">UPLOAD_ERR_EXTENSION</td>
      <td style="text-align:left">php&#x7684;extension&#x505C;&#x6B62;&#x4E86;&#x4E0A;&#x50B3;&#x7684;&#x5DE5;&#x4F5C;</td>
    </tr>
  </tbody>
</table>

### copy\(\)暫存檔存放暫存路徑

語法：copy\("來源路徑及檔名","複製之目的路徑及檔名"\)

```php
//例如
$dir = "images";                        //路徑名
$from = $_FILES["upFile"]["tmp_name"];    //來源路徑及檔名
$to = "$dir/".$_FILES["upFile"]["name"]; //複製之目的路徑及檔名
copy($from, $to);
echo "上傳成功～<br>";
```

### move\_uploaded\_file\(\)將暫存檔移到指定路徑

語法：move\_uploaded\_file\("來源路徑及檔名","複製之目的路徑及檔名"\)

```php
//例如
$dir = "images";                        //路徑名
$from = $_FILES["upFile"]["tmp_name"];    //來源路徑及檔名
$to = "$dir/".$_FILES["upFile"]["name"]; //複製之目的路徑及檔名
move_uploaded_file($from, $to);
echo "上傳成功～<br>";
```

### 範例

對應範例檔案「fileUpload.html」、「fileUpload.php」

{% tabs %}
{% tab title="1" %}
錯誤代號

```php
echo "帳號：", $_POST["memId"], "<br>";
switch($_FILES["upFile"]["error"];){
    case 0://上傳成功
        //============檢查資料夾是否存在
        $dir = "images";//路徑名
        if(file_exists($dir)==false){
            //沒有這個資料夾，創建一個資料夾
            mkdir($dir);//make directory
        }
        $from = $_FILES["upFile"]["tmp_name"];
        $to = "$dir/".$_FILES["upFile"]["name"]; //images/smile.gif
        copy($from, $to);
        echo "上傳成功～<br>";
    break;
    case 1: //php.ini系統上限設定為2M
        echo "上傳檔案太大，不得超過",ini_get("upload_max_filesize"),"<br>";
    break;
    case 2: //fileUpload指定上限(小於等於ini系統上限)為123456 Bytes
        echo "上傳檔案太大",$_POST["MAX_FILE_SIZE"],"<br>";
    break;
    case 3:
        echo "檔案損毀或丟失<br>";
    break;
    case 4:
        echo "檔案未選取<br>";
    break;
    default:
        echo "系統錯誤，請通知維護人員<br>";
}
```
{% endtab %}

{% tab title="2" %}
錯誤代碼

```php
echo "帳號：", $_POST["memId"], "<br>";
switch($_FILES["upFile"]["error"]){
    case UPLOAD_ERR_OK://上傳成功
        //============檢查資料夾是否存在
        $dir = "images";//路徑名
        if(file_exists($dir)==false){
            //沒有這個資料夾，創建一個資料夾
            mkdir($dir);//make directory
        }
        $from = $_FILES["upFile"]["tmp_name"];
        $to = "$dir/".$_FILES["upFile"]["name"]; //images/smile.gif
        copy($from, $to);
        echo "上傳成功～<br>";
    break;
    case UPLOAD_ERR_INI_SIZE: //php.ini系統上限設定為2M
        echo "上傳檔案太大，不得超過",ini_get("upload_max_filesize")," Bytes<br>";
    break;
    case UPLOAD_ERR_FORM_SIZE: //fileUpload指定上限(小於等於ini系統上限)為123456 Bytes
        echo "上傳檔案太大","不得超過",$_POST["MAX_FILE_SIZE"]," Bytes<br>";
    break;
    case UPLOAD_ERR_PARTIAL:
        echo "檔案損毀或丟失<br>";
    break;
    case UPLOAD_ERR_NO_FILE:
        echo "檔案未選取<br>";
    break;
    default:
        echo "系統錯誤，請通知維護人員<br>";
}
```
{% endtab %}
{% endtabs %}

## 上傳多個檔案

* 標籤換成`<input type="file" name="upFile[]"><br>`  「`name="upFile[]"`」陣列型態。
* 搭配迴圈寫

{% hint style="info" %}
input:file的屬性  
`<input type="file" name="upFile[]" multiple accept="image/*">`  
「`name="upFile[]"`」：陣列型態  
「`multiple`」：可複選檔案  
「`accept="image/*"`」：指定檔案格式
{% endhint %}

### 範例

搭配檔案「fileUploadMany.html」、「fileUploadMany.php」

```markup
<!--HTML-->
<form action="fileUploadMany.php" method="post" enctype="multipart/form-data">
    帳號 <input type="text" name="memId"><br>
    姓名<input type="text" name="memName"><br>	
    大頭貼一 <input type="file" name="upFile[]"><br>
    大頭貼二 <input type="file" name="upFile[]"><br>
    大頭貼三 <input type="file" name="upFile[]"><br>
    <input type="submit" value="OK">
</form>  
```

```php
//PHP
<?php 
foreach($_FILES["upFile"]["error"] as $i => $data){
    switch($_FILES["upFile"]["error"][$i]){
        case UPLOAD_ERR_OK://上傳成功
            //============檢查資料夾是否存在
            $dir = "images";//路徑名
            if(file_exists($dir)==false){
                //沒有這個資料夾，創建一個資料夾
                mkdir($dir);//make directory
            }
            $from = $_FILES["upFile"]["tmp_name"][$i];
            $to = "$dir/".$_FILES["upFile"]["name"][$i]; //images/smile.gif
            copy($from, $to);
            echo "上傳成功～<br>";
        break;
        case UPLOAD_ERR_INI_SIZE: //php.ini系統上限設定為2M
            echo "上傳檔案太大，不得超過",ini_get("upload_max_filesize")," Bytes<br>";
        break;
        case UPLOAD_ERR_FORM_SIZE: //fileUpload指定上限(小於等於ini系統上限)為123456 Bytes
            echo "上傳檔案太大","不得超過",$_POST["MAX_FILE_SIZE"]," Bytes<br>";
        break;
        case UPLOAD_ERR_PARTIAL:
            echo "檔案損毀或丟失<br>";
        break;
        case UPLOAD_ERR_NO_FILE:
            echo "檔案未選取<br>";
        break;
        default:
            echo "系統錯誤，請通知維護人員<br>";
    }
}
?>
```

