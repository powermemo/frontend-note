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
      <td style="text-align:left">open(&quot;method&quot;,&quot;url&quot;,async)</td>
      <td style="text-align:left">&#x958B;&#x555F;&#x5C0D;&#x4F3A;&#x670D;&#x7AEF;&#x7684;&#x9023;&#x7D50;</td>
    </tr>
    <tr>
      <td style="text-align:left">send(&quot;content&quot;)</td>
      <td style="text-align:left">&#x5411;&#x4F3A;&#x670D;&#x5668;&#x767C;&#x9001;&#x8ACB;&#x6C42;&#xFF0C;&#x4E26;&#x5C07;&#x8CC7;&#x6599;&#x9001;&#x5230;&#x4F3A;&#x670D;&#x5668;&#x7AEF;</td>
    </tr>
    <tr>
      <td style="text-align:left">setRequestHeader(&quot;head&quot;,&quot;value&quot;)</td>
      <td style="text-align:left">&#x8A2D;&#x5B9A;HTTP&#x8ACB;&#x6C42;&#x7684;&#x8ACB;&#x6C42;&#x6A19;&#x982D;&#x3002;</td>
    </tr>
  </tbody>
</table>

