---
description: 參照講義p.39~p.50、p.51~p.74
---

# SELECT FROM WHERE

## SELECT FROM

* 顯示表格全部欄位及資料。 `SELECT * FROM` 表格名稱; 
* 顯示指定欄位及其底下的資料。 SELECT 欄位名稱1,欄位名稱2,欄位名稱3... FROM 表格名稱; 
* 設定欄位名稱別名，以逗號區隔欄位。 SELECT 欄位名稱1 欄位別名1,欄位名稱2 欄位別名2,欄位名稱3 欄位別名3... FROM 表格名稱; 
* 欄位合併 SELECT concat\(欄位名稱1,’用甚麼連結\(這是選填\)’,欄位名稱2\) 合併後的欄位名稱 FROM 表格名稱; 
* 重複資料列排除\(DISTINCT\)，例如想知道公司的部門有哪些，用員工資料查詢。 SELECT `DISTINCT` 欄位名稱 FROM 表格名稱; 
* 查詢結果傳回資料筆數\(LIMIT\) SELECT 欄位名稱1,欄位名稱2,欄位名稱3... FROM 表格名稱 `LIMIT` \(選填\)跳過開始的?筆資料,顯示?筆資料;



## SELECT FROM WHERE

* 條件篩選 SELECT ... FROM ... `WHERE` 條件ex. empno&gt;10;
  * 比較運算子=、&gt;=、&lt;=、&gt;、&lt;、&lt;&gt;
  * 邏輯運算子AND、OR、NOT
  * 特定運算子BETWEEN、IN、LIKE、IS NULL
  * 特定運算子:

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left">BETWEEN <em>x1</em> AND <em>x2</em>
      </th>
      <th style="text-align:left">IN(<em>x1,x2,...,xn</em>)</th>
      <th style="text-align:left">LIKE</th>
      <th style="text-align:left">IS NULL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#x89E3;&#x8AAA;</td>
      <td style="text-align:left">
        <p>&#x5728;&#x67D0;&#x7BC4;&#x570D;(x1~x2)&#x5167;</p>
        <p>&#x4F8B;&#x5982;1000~3000</p>
        <p>&#x5305;&#x542B;x1&#x548C;x2&#x7684;&#x503C;</p>
      </td>
      <td style="text-align:left">
        <p>&#x5728;&#x67D0;&#x500B;&#x5217;&#x8209;&#x7684;&#x96C6;&#x5408;&#x4E2D;(IN&#x7684;&#x62EC;&#x865F;&#x5167;&#x7684;&#x6578;)
          <br
          />
        </p>
        <p>x1&#x6216;x2...&#x6216;xn</p>
      </td>
      <td style="text-align:left">
        <p>&#x6A21;&#x7CCA;&#x6BD4;&#x5C0D;</p>
        <p>&#x2018;%x&#x2019;&#x4EFB;&#x610F;&#x9577;&#x5EA6;&#x5B57;&#x5143;</p>
        <p>&#x2018;_x&#x2019;&#x4E00;&#x500B;&#x5B57;&#x5143;</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">&#x7BC4;&#x4F8B;</td>
      <td style="text-align:left"><code>WHERE </code><em><code>sal </code></em><code>BETWEEN </code><em><code>2000 </code></em><code>AND </code><em><code>3500;</code></em>
      </td>
      <td style="text-align:left"><code>WHERE </code><em><code>code </code></em><code>IN (</code><em><code>&apos;A&apos;</code></em><code>,</code><em><code>&apos;B&apos;</code></em><code>,&apos;</code><em><code>C&apos;</code></em><code>);</code>
      </td>
      <td style="text-align:left">
        <p><code>WHERE </code><em><code>ename </code></em><code>LIKE</code><em><code> &apos;_A%&apos;;</code></em>
        </p>
        <p>&#x610F;&#x601D;&#x662F;&#x7B2C;&#x4E8C;&#x500B;&#x5B57;&#x662F;A&#xFF0C;%&#x8868;*&#x4EFB;&#x610F;&#x5B57;</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">&#x7BC4;&#x4F8B;&#x4E8C;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p><code>WHERE </code><em><code>content </code></em><code>LIKE </code><em><code>&apos;%3\%%&apos; </code></em><b><code>ESCAPE </code></b><em><code>&apos;\&apos;</code></em><code>;</code>
        </p>
        <p>&#x8DF3;&#x812B;&#x5B57;&#x5143;&#x300C;\&#x300D;-- 3%</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

* .

  * 列舉式CASE\(以下用例子\) SELECT ... FROM ... WHERE `CASE` 欄位名 　　　　　　WHEN '條件1' THEN 執行1 　　　　　　WHEN '條件2' THEN 執行2 　　　　　　WHEN '條件3' THEN 執行3 　　　　　　ELSE 執行4 　　　　　END 執行後新欄位名稱;-- \(以下代入例子\)  `WHERE CASE job 　　　　　　WHEN 'President' THEN Sal*1.5 　　　　　　WHEN 'Manager' THEN Sal*1.3 　　　　　　WHEN 'Analyst' THEN Sal*1.2 　　　　　　ELSE Sal*1 　　　　　END sal;`



  * 條件式CASE  
    SELECT ...  
    FROM ...  
    WHERE  
    　　CASE 欄位名 BETWEEN x1 AND y1 THEN 執行1  
    　　　　　欄位名 BETWEEN x2 AND y2 THEN 執行2  
    　　　　　欄位名 BETWEEN x3 AND y3 THEN 執行3  
    　　　　　ELSE 執行4  
    　　　　END 執行後新欄位名稱;-- \(以下帶入例子\)

  
    `WHERE  
    　　CASE sal BETWEEN 0    AND 1000 THEN ‘A’  
    　　　　　sal BETWEEN 1001 AND 2000 THEN ‘B’  
    　　　　　sal BETWEEN 2001 AND 3000 THEN ‘C’  
    　　　　　ELSE ‘D’  
    　　　　END sal;`

## 條件篩選ORDER BY

SELECT ...  
FROM ...  
WHERE  …  
ORDER BY 欄位名稱 \| 欄位數 \| 欄位別名 \[ASC升冪預設 \| DESC降冪\];

以下範例

{% tabs %}
{% tab title="降冪" %}
範例一：對薪資做降冪排序  
`SELECT empno, ename, sal  
FROM emp  
WHERE deptno = 10  
ORDER BY sal DESC;🔶`
{% endtab %}

{% tab title="第x欄" %}
範例二：對第三直排做排序  
`SELECT *  
 FROM emp   
WHERE deptno = 20   
ORDER BY 3;🔶`
{% endtab %}

{% tab title="多欄" %}
範例三：多欄排序，以「逗號」分隔

* 對 \[部門\] 做升冪排序
* 對 \[職稱\] 做升冪排序
* 對 \[第六直欄\] 做降冪排序
* 對 \[第一欄\]做升冪排序

`SELECT *  
FROM emp  
ORDER BY deptno, job, 6 DESC, 1;🔶`
{% endtab %}

{% tab title="LIMIT" %}
範例四：只顯示指定筆數  
\(例如有14橫列，LIMIT 5 就是指  只顯示前面五筆。\)

`SELECT ename, sal, job  
FROM emp  
ODER BY sal DESC🔷  
LIMIT 5;🔶`
{% endtab %}
{% endtabs %}

{% hint style="info" %}
不在「SELECT」的欄位也可以做排序。
{% endhint %}

