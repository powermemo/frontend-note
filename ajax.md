---
description: 一種非同步的技術，它不是新語言
---

# Ajax

## 建立Ajax核心物件 - XMLHttpRequest

```aspnet
var xhr = newXMLHttpRequest();
```

## XMLHttpRequest methods方法

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x65B9;&#x6CD5;&#x540D;&#x7A31;</th>
      <th style="text-align:left">&#x8AAA;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">abort()</td>
      <td style="text-align:left">&#x505C;&#x6B62;&#x7576;&#x524D;&#x8ACB;&#x6C42;</td>
    </tr>
    <tr>
      <td style="text-align:left">getAllResponseHeaders()</td>
      <td style="text-align:left">
        <p>&#x53D6;&#x5F97;HTTP&#x7684;&#x6240;&#x6709;&#x56DE;&#x61C9;&#x6A19;&#x982D;</p>
        <p>ex. &lt;meta charset...&gt;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">getResponseHeader(&quot;header&quot;)</td>
      <td style="text-align:left">&#x53D6;&#x5F97;&#x67D0;&#x7279;&#x5B9A;HTTP&#x56DE;&#x61C9;&#x4E4B;&#x6A19;&#x982D;/&#x5B57;&#x4E32;&#x503C;</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>open(&quot;method&quot;,&quot;url&quot;,async)</b>
      </td>
      <td style="text-align:left">&#x958B;&#x555F;&#x5C0D;&#x4F3A;&#x670D;&#x7AEF;&#x7684;&#x9023;&#x7D50;</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>send(&quot;content&quot;)</b>
      </td>
      <td style="text-align:left">&#x5411;&#x4F3A;&#x670D;&#x5668;&#x767C;&#x9001;&#x8ACB;&#x6C42;&#xFF0C;&#x4E26;&#x5C07;&#x8CC7;&#x6599;&#x9001;&#x5230;&#x4F3A;&#x670D;&#x5668;&#x7AEF;</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>setRequestHeader(&quot;head&quot;,&quot;value&quot;)</b>
      </td>
      <td style="text-align:left">&#x8A2D;&#x5B9A;HTTP&#x8ACB;&#x6C42;&#x7684;&#x8ACB;&#x6C42;&#x6A19;&#x982D;&#x3002;</td>
    </tr>
  </tbody>
</table>

### open\("_method_","_url_",_async_\)

開啟對伺服端的連結

* method參數：如GET或POST
  * POST的使用時機
    * 不想用到cache中的檔案
    * 要傳送的資料太大
    * 安全性考量
* url參數：指定所要存取檔案的位置
* async參數：決定採用非同步傳輸或不採用
  * `true` 非同步  \|   false 同步

### send\("_content_"\)

向伺服器發送請求，並將資料送到伺服器端。

* send\(null\)：open\(\)的method為GET
* send\(data\_info\)：open\(\)的method為POST
  * data\_info為自定義
  * 格式："欄名1=值**&**欄名2=值**&**..."

### setRequestHeader\(_header_,_value_\)

method為POST時使用，設定HTTP請求的請求標頭。  
POST一定要設哦！

* header：Http的標頭名稱
* value：標頭名稱的值

```aspnet
xhr.setRequestHeader("content-Type","application/x-www-form-urlencoded")
```

## XMLHttpRequest attributes屬性

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x5C6C;&#x6027;&#x540D;&#x7A31;</th>
      <th style="text-align:left">&#x8AAA;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">readyState</td>
      <td style="text-align:left">
        <p>&#x8ACB;&#x6C42;&#x8655;&#x7406;&#x72C0;&#x614B;</p>
        <p>ex. 0&#x2192;1&#x2192;2...</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">onreadystatechange</td>
      <td style="text-align:left">
        <p>&#x8ACB;&#x6C42;&#x7684;&#x8655;&#x7406;&#x72C0;&#x614B;&#x6539;&#x8B8A;&#x6642;&#x61C9;&#x57F7;&#x884C;&#x7684;&#x4E8B;&#x4EF6;&#x8655;&#x5668;</p>
        <p>ex.readyState&#x72C0;&#x614B; 0&#x2192;1&#x2192;2...</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">status</td>
      <td style="text-align:left">&#x4F3A;&#x670D;&#x5668;&#x56DE;&#x50B3;&#x7684;Http&#x72C0;&#x614B;&#x78BC;</td>
    </tr>
    <tr>
      <td style="text-align:left">statusText</td>
      <td style="text-align:left">&#x4F3A;&#x670D;&#x5668;&#x56DE;&#x50B3;&#x7684;Http&#x72C0;&#x614B;&#x6587;&#x5B57;&#x8A0A;&#x606F;</td>
    </tr>
    <tr>
      <td style="text-align:left">responseText</td>
      <td style="text-align:left">&#x4F3A;&#x670D;&#x5668;&#x7684;&#x56DE;&#x50B3;&#x8CC7;&#x6599;&#xFF0C;&#x56DE;&#x61C9;&#x7684;&#x5167;&#x5BB9;&#x70BA;&#x4E00;&#x500B;&#x5B57;&#x4E32;</td>
    </tr>
    <tr>
      <td style="text-align:left">responseXML</td>
      <td style="text-align:left">&#x4F3A;&#x670D;&#x5668;&#x7684;&#x56DE;&#x50B3;&#x8CC7;&#x6599;&#xFF0C;&#x56DE;&#x61C9;&#x7684;&#x5167;&#x5BB9;&#x70BA;XML
        Document</td>
    </tr>
  </tbody>
</table>

