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

## PDO指令\[官網[連結](https://www.php.net/manual/en/pdo.constants.php)\]

利用「PDO」存取SQL資料，是安全性較佳的方法。  
PDO可連結更多資料庫系統、PDO可避免SQL injection攻擊。

