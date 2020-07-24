# 設定&安裝

## IIS

### 開啟

🔶控制台 &gt; 程式集 &gt; 開始或關閉windows功能  
\(要記得打開CGI，因為預設不會打勾\)

![](../.gitbook/assets/image%20%281%29.png)

### 資料夾在哪裡

C:\inetput\wwwroot

### 我要怎麼在裡面新增檔案

對資料夾按右鍵 &gt; 內容 &gt; 安全性 &gt; 編輯 &gt; user....blrablrablra &gt; \[完全控制\] 打勾

### 我的網域是甚麼

![](../.gitbook/assets/image%20%2837%29.png)

網路和共用中心 &gt; 網路狀態 &gt; 網路連線詳細資料

方法二－命令提示字元  
cmd打開命令提示字元 &gt; 輸入指令「ipconfig」

## PHP

### 下載

官網\[[https://www.php.net/](https://www.php.net/)\]

![](../.gitbook/assets/image%20%2810%29.png)

* 官網 &gt; Download &gt;  [Windows downloads](https://windows.php.net/download#php-7.4)
* Which version do I choose?

  IIS

  If you are using PHP as FastCGI with IIS you should use the **Non-Thread Safe \(NTS\)** versions of PHP.

* 點選ZIP檔
* 2020-06-24是這個版本 **VC15 x64 Non Thread Safe \(2020-Jun-09 17:07:39\)**[Zip](https://windows.php.net/downloads/releases/php-7.4.7-nts-Win32-vc15-x64.zip) \[24.82MB\]



### 安裝

* zip檔解壓縮之後放C槽。
* 開啟IIS「處理常式對應」  &gt; 「新增模組對應」 &gt; 「編輯模組對應」

![](../.gitbook/assets/image%20%285%29.png)

![Fast\_Cgi\_PHP&#x662F;&#x81EA;&#x5B9A;&#x7FA9;&#xFF0C;&#x96A8;&#x4FBF;&#x4F60;&#x60F3;&#x53D6;&#x751A;&#x9EBC;&#x540D;&#x5B57;&#x3002;](../.gitbook/assets/image%20%2819%29.png)

