# 設定&安裝

## IIS

### 開啟

🔶控制台 > 程式集 > 開始或關閉windows功能\
(要記得打開CGI，因為預設不會打勾)

![](<../.gitbook/assets/image (1).png>)

### 資料夾在哪裡

C:\inetput\wwwroot

### 我要怎麼在裡面新增檔案

對資料夾按右鍵 > 內容 > 安全性 > 編輯 > user....blrablrablra > \[完全控制] 打勾

### 我的網域是甚麼

![](<../.gitbook/assets/image (37).png>)

網路和共用中心 > 網路狀態 > 網路連線詳細資料

方法二－命令提示字元\
cmd打開命令提示字元 > 輸入指令「ipconfig」

## PHP

### 下載

官網\[[https://www.php.net/](https://www.php.net)]

![](<../.gitbook/assets/image (10).png>)

* 官網 > Download >  [Windows downloads](https://windows.php.net/download#php-7.4)
*   Which version do I choose?

    IIS

    If you are using PHP as FastCGI with IIS you should use the **Non-Thread Safe (NTS)** versions of PHP.
* 點選ZIP檔
* 2020-06-24是這個版本\
  **VC15 x64 Non Thread Safe (2020-Jun-09 17:07:39)**Zip \[24.82MB]



### 安裝

* zip檔解壓縮之後放C槽。
* 開啟IIS「處理常式對應」 \
  \> 「新增模組對應」 > 「編輯模組對應」

![](<../.gitbook/assets/image (5).png>)

![Fast\_Cgi\_PHP是自定義，隨便你想取甚麼名字。](<../.gitbook/assets/image (19).png>)

### 環境設置－組態檔(php.ini)

改變預設值(例如時區)的步驟，以下是以「更改為台灣時區」作為範本

{% tabs %}
{% tab title="更改時區" %}
1. 到C槽(你存放的位置)php資料夾找到「php.ini-development」檔案，複製一份
2. 將複製的那份檔案，更改副檔名為「php.ini」
3. 修改檔案內容的「**date.timezone=**」，後面加上「Asia/Taipei」\
   再砍掉前面註解符號「;」

p.s. 若時區無更動，IIS重新整理。

![](<../.gitbook/assets/image (16).png>)


{% endtab %}

{% tab title="短標籤可以作用" %}
短標籤就是把「`<?php?>`」可以縮寫成「`<??>`」\
(1.2.如果之前做過，就不用再做一次了。)

```php
<?=$name?>
```

1. 到C槽(你存放的位置)php資料夾找到「php.ini-development」檔案，複製一份
2. 將複製的那份檔案，更改副檔名為「php.ini」
3. 修改檔案內容的「**short\_open\_tag=On**」
{% endtab %}
{% endtabs %}

{% hint style="info" %}
【非英文字串】使用「mbstring」。預設是關的，要打開....

1. php.ini找「**extension=mbstring**」，並把「;」註解拿掉
2. php.ini找「**extension\_dir="ext"**」，把「;」註解拿掉\
   將等號後面的值改為**資料夾位置**ex.「C:\php-7.4.7\ext」
3. 打開IIS，重新啟動。
{% endhint %}

以下的(這一條)mac電腦都可以不用弄(已經好了)。

{% hint style="info" %}
【引用PDO指令】(一種安全性較佳的指令)

1. 找到ini檔，把以下註解「;」拿掉\
   **extension = mysqli**\
   **extension = pdo\_mysql**
2. 重整IIS
{% endhint %}

{% hint style="info" %}
【Server端取得上傳檔案】

1. 允許上傳：**file\_uploads** = on
2. 上傳暫存區：**upload\_tmp\_dir** = C:\php位置....\tmp
3. 上傳容量上限：**upload\_max\_filesize** = 2M
{% endhint %}

{% hint style="info" %}
【使用phpMyAdmin】(一種網頁版的操作介面)

1. 下載phpMyAdmin(老師提供)，丟到wwwroot資料夾。
2. 到IIS打開phpMyAdmin資料夾的「index.php」檔案。
{% endhint %}

