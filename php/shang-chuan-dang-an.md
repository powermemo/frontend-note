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



### $\_FILES\[\]取得上傳資料



### $\_FILES\["上傳檔案欄位"\]\["error"\]錯誤代碼





