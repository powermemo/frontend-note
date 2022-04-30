---
description: 參照講義p.19、p.31~p.38
---

# 操作

## 介面分為\[圖形化使用者介面]、\[命列列工具列]

我不知道你們啦，我個人用圖形化（workbench）用很爽==



##

## 基本指令

* 備註的方法單行註解用兩槓加一個空白「-- 」；\
  多行註解跟CSS一樣「/\*\*/」
* 講義p.32

| 指令                         | 說明                                                | 範例                    |
| -------------------------- | ------------------------------------------------- | --------------------- |
| SHOW DATABASES;            | 列出目前伺服器所有的資料庫。                                    | `SHOW DATABASES;`     |
| USE _\[ 資料庫名稱 ]_;          | <p>斜體字中括號[database]是資料庫的名字。</p><p>設定目前存取的資料庫。</p> | `USE demo;`           |
| SHOW TABLES;               | 列出預設資料庫所有資料表。                                     | `SHOW TABLES;`        |
| DESC\[RIBE]  _\[欄位名稱]_     | 列出指定資料表欄位資訊。                                      | `DESCRIBE Dname ;`    |
| SELECT \* FROM _\[資料表名稱]_; | <p>列出資料表資料。</p><p>「*」表全部。</p>                     | `SELECT * FROM dept;` |

## 建立資料庫

{% tabs %}
{% tab title="命令列工具列" %}
* **CREATE DATABASE** _\[資料庫名稱]_ ;\
  &#x20;\-- 建立資料庫\
  &#x20;\-- 例如 `CREATE DATABASE mydb;`
* **SOURCE** _\[路徑名稱]_\
  &#x20;\-- 執行一個命令檔案（後面加上分號會無效哦！）\
  　（匯入資料庫）\
  &#x20;\-- 例如 `SOURCE c:\mysql_demobld.sql`
* DROP\
  捨棄資料庫\



{% endtab %}

{% tab title="圖形化使用者介面" %}
![建立資料庫](<../.gitbook/assets/image (15).png>)

![匯入資料庫：file>Run SQL Script](<../.gitbook/assets/image (38).png>)

{% hint style="info" %}
「Run SQL Script」按下去後會彈出一個視窗\
記得在第一個input輸入資料庫名稱。
{% endhint %}
{% endtab %}
{% endtabs %}
