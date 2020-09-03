---
description: 參照講義p.19、p.31~p.38
---

# 操作

## 介面分為\[圖形化使用者介面\]、\[命列列工具列\]

我不知道你們啦，我個人用圖形化（workbench）用很爽==



## 

## 基本指令

* 備註的方法單行註解用兩槓加一個空白「-- 」； 多行註解跟CSS一樣「/\*\*/」
* 講義p.32

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x6307;&#x4EE4;</th>
      <th style="text-align:left">&#x8AAA;&#x660E;</th>
      <th style="text-align:left">&#x7BC4;&#x4F8B;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">SHOW DATABASES;</td>
      <td style="text-align:left">&#x5217;&#x51FA;&#x76EE;&#x524D;&#x4F3A;&#x670D;&#x5668;&#x6240;&#x6709;&#x7684;&#x8CC7;&#x6599;&#x5EAB;&#x3002;</td>
      <td
      style="text-align:left"><code>SHOW DATABASES;</code>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">USE <em> [ &#x8CC7;&#x6599;&#x5EAB;&#x540D;&#x7A31; ]</em>;</td>
      <td style="text-align:left">
        <p>&#x659C;&#x9AD4;&#x5B57;&#x4E2D;&#x62EC;&#x865F;[database]&#x662F;&#x8CC7;&#x6599;&#x5EAB;&#x7684;&#x540D;&#x5B57;&#x3002;</p>
        <p>&#x8A2D;&#x5B9A;&#x76EE;&#x524D;&#x5B58;&#x53D6;&#x7684;&#x8CC7;&#x6599;&#x5EAB;&#x3002;</p>
      </td>
      <td style="text-align:left"><code>USE demo;</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">SHOW TABLES;</td>
      <td style="text-align:left">&#x5217;&#x51FA;&#x9810;&#x8A2D;&#x8CC7;&#x6599;&#x5EAB;&#x6240;&#x6709;&#x8CC7;&#x6599;&#x8868;&#x3002;</td>
      <td
      style="text-align:left"><code>SHOW TABLES;</code>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">DESC[RIBE] <em>[&#x6B04;&#x4F4D;&#x540D;&#x7A31;]</em> 
      </td>
      <td style="text-align:left">&#x5217;&#x51FA;&#x6307;&#x5B9A;&#x8CC7;&#x6599;&#x8868;&#x6B04;&#x4F4D;&#x8CC7;&#x8A0A;&#x3002;</td>
      <td
      style="text-align:left"><code>DESCRIBE Dname ;</code>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">SELECT * FROM <em>[&#x8CC7;&#x6599;&#x8868;&#x540D;&#x7A31;]</em>;</td>
      <td
      style="text-align:left">
        <p>&#x5217;&#x51FA;&#x8CC7;&#x6599;&#x8868;&#x8CC7;&#x6599;&#x3002;</p>
        <p>&#x300C;*&#x300D;&#x8868;&#x5168;&#x90E8;&#x3002;</p>
        </td>
        <td style="text-align:left"><code>SELECT * FROM dept;</code>
        </td>
    </tr>
  </tbody>
</table>

## 建立資料庫

{% tabs %}
{% tab title="命令列工具列" %}
* **CREATE DATABASE** _\[資料庫名稱\]_ ;  -- 建立資料庫  -- 例如 `CREATE DATABASE mydb;`
* **SOURCE** _\[路徑名稱\]_  -- 執行一個命令檔案（後面加上分號會無效哦！） 　（匯入資料庫）  -- 例如 `SOURCE c:\mysql_demobld.sql`
* DROP 捨棄資料庫 
{% endtab %}

{% tab title="圖形化使用者介面" %}
![&#x5EFA;&#x7ACB;&#x8CC7;&#x6599;&#x5EAB;](../.gitbook/assets/image%20%2815%29.png)

![&#x532F;&#x5165;&#x8CC7;&#x6599;&#x5EAB;&#xFF1A;file&amp;gt;Run SQL Script](../.gitbook/assets/image%20%2838%29.png)

{% hint style="info" %}
「Run SQL Script」按下去後會彈出一個視窗  
記得在第一個input輸入資料庫名稱。
{% endhint %}
{% endtab %}
{% endtabs %}

