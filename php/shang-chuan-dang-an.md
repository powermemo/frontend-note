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

* 檔案名稱：`$_FILES["上傳檔案欄位"]["name"]`
* 暫存檔名和路徑：`$_FILES["上傳檔案欄位"]["tmp_name"]`
* 檔案尺寸：`$_FILES["上傳檔案欄位"]["size"]`
* 檔案種類：`$_FILES["上傳檔案欄位"]["type"]`
* 上傳檔案時發生的錯誤代碼：`$_FILES["上傳檔案欄位"]["error"]`。

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

### 

