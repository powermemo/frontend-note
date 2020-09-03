---
description: 參照講義p.75~p.98
---

# 資料型態、FUNCTION

## 種類\(p.75\)

1. 基本資料型態
   1. **字串**資料
   2. **數值**資料
2. 導出型資料型態
   1. **日期**／時間資料

資料型態大概有那些\(括號裡面都是相同的只是寫法不同\)：

| 數值資料 | 日期時間資料 | 文數字資料 |
| :--- | :--- | :--- |
| TINYINT | **`DATE`** | CHAR\(M\) |
| SMALLINT | **`DATETIME`** | **`VARCHAR(M)`** |
| MEDIUMINT | TIMESTAMP | TINYBLOB, TINYTEXT |
| **`INT`**, INTEGER | TIME | BLOB, TEXT |
| BIGINT | YEAR | MEDIUMBLOB, MEDIUMTEXT |
| FLOAT\(P\) |  | LONGBLOB, LONGTEXT |
| FLOAT |  |  |
| DOUBLE \[PRECISION\], item REAL |  |  |
| **`DECIMAL(M,D), NUMERIC(M,D)`** |  |  |

{% hint style="info" %}
* 這頁面列出的項目都只是**部分**或常用的，並不是全部的函式與指令！
* 看到這樣的  **`字樣`**  表示常用w。
{% endhint %}

## 【字串函數】\(p.85\)

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x51FD;&#x6578;</th>
      <th style="text-align:left">&#x529F;&#x80FD;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">LENGTH(<em>str</em>)</td>
      <td style="text-align:left">&#x5B57;&#x4E32;&#x9577;&#x5EA6;</td>
    </tr>
    <tr>
      <td style="text-align:left">CHAR_LENGTH(<em>str</em>)</td>
      <td style="text-align:left">&#x5B57;&#x5143;&#x500B;&#x6578;</td>
    </tr>
    <tr>
      <td style="text-align:left">LCASE(str) | LOWER(str)</td>
      <td style="text-align:left">&#x8F49;&#x5C0F;&#x5BEB;&#x5B57;&#x6BCD;</td>
    </tr>
    <tr>
      <td style="text-align:left">UCASE(str) | UPPER(str)</td>
      <td style="text-align:left">&#x8F49;&#x5927;&#x5BEB;&#x5B57;&#x6BCD;</td>
    </tr>
    <tr>
      <td style="text-align:left">ASCII(str)</td>
      <td style="text-align:left">&#x56DE;&#x50B3;ASCII&#x78BC;</td>
    </tr>
    <tr>
      <td style="text-align:left"><b><code>CONCAT(str1, str2,...)</code></b>
      </td>
      <td style="text-align:left">&#x5B57;&#x4E32;&#x9023;&#x7D50;</td>
    </tr>
    <tr>
      <td style="text-align:left">FIELD(str1, str2,...)</td>
      <td style="text-align:left">str&#x5728;str list&#x7684;&#x4F4D;&#x7F6E;</td>
    </tr>
    <tr>
      <td style="text-align:left">INSERT(str,pos,len,newstr)</td>
      <td style="text-align:left">&#x6307;&#x5B9A;&#x5340;&#x9593;&#x63D2;&#x5165;&#x4E00;&#x5B57;&#x4E32;</td>
    </tr>
    <tr>
      <td style="text-align:left">LEFT(str,len)</td>
      <td style="text-align:left">&#x7531;&#x5DE6;&#x81F3;&#x53F3;&#x50B3;&#x56DE;&#x6307;&#x5B9A;&#x5B57;&#x5143;&#x6578;</td>
    </tr>
    <tr>
      <td style="text-align:left">RIGHT(str,len)</td>
      <td style="text-align:left">&#x7531;&#x53F3;&#x81F3;&#x5DE6;&#x50B3;&#x56DE;&#x6307;&#x5B9A;&#x5B57;&#x5143;&#x6578;</td>
    </tr>
    <tr>
      <td style="text-align:left">REVERSE(str)</td>
      <td style="text-align:left">&#x5B57;&#x4E32;&#x53CD;&#x8F49;</td>
    </tr>
    <tr>
      <td style="text-align:left">LPAD(str,len,padstr)</td>
      <td style="text-align:left">&#x5B57;&#x4E32;&#x4E0D;&#x8DB3;&#x6307;&#x5B9A;&#x5B57;&#x5143;&#x5411;&#x5DE6;&#x88DC;&#x9F4A;</td>
    </tr>
    <tr>
      <td style="text-align:left">RPAD(str,len,padstr)</td>
      <td style="text-align:left">&#x5B57;&#x4E32;&#x4E0D;&#x8DB3;&#x6307;&#x5B9A;&#x5B57;&#x5143;&#x5411;&#x53F3;&#x88DC;&#x9F4A;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b><code>SUBSTRING(str,pos)</code></b>
        </p>
        <p>SUBSTRING(str FROM pos)</p>
        <p><b><code>SUBSTRING(str, pos,len)</code></b>
        </p>
        <p>SUBSTRING(str FROM pos FOR len)</p>
      </td>
      <td style="text-align:left">&#x64F7;&#x53D6;&#x5B57;&#x4E32;&#x90E8;&#x5206;&#x5B57;&#x5143;</td>
    </tr>
    <tr>
      <td style="text-align:left">REPEAT(str,count)</td>
      <td style="text-align:left">&#x6307;&#x5B9A;&#x5B57;&#x4E32;&#x91CD;&#x8907;&#x6307;&#x5B9A;&#x6B21;&#x6578;</td>
    </tr>
    <tr>
      <td style="text-align:left">SPACE(N)</td>
      <td style="text-align:left">&#x7A7A;&#x767D;&#x5B57;&#x5143;&#x91CD;&#x8907;&#x6307;&#x5B9A;&#x6B21;&#x6578;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>INSTR(str,substr)</p>
        <p>LOCATE(substr,str[,pos])</p>
      </td>
      <td style="text-align:left">&#x50B3;&#x56DE;&#x5B57;&#x5143;&#x5728;&#x5B57;&#x4E32;&#x4E2D;&#x7684;&#x4F4D;&#x7F6E;</td>
    </tr>
    <tr>
      <td style="text-align:left">REPLACE(str, from_str,to_str)</td>
      <td style="text-align:left">&#x65B0;&#x5B57;&#x4E32;&#x66FF;&#x4EE3;&#x820A;&#x5B57;&#x4E32;</td>
    </tr>
    <tr>
      <td style="text-align:left">LTRIM(str)</td>
      <td style="text-align:left">&#x53BB;&#x9664;&#x5B57;&#x4E32;&#x7D44;&#x5DE6;&#x908A;&#x7A7A;&#x767D;</td>
    </tr>
    <tr>
      <td style="text-align:left">RTRIM(str)</td>
      <td style="text-align:left">&#x53BB;&#x9664;&#x5B57;&#x4E32;&#x7D44;&#x53F3;&#x908A;&#x7A7A;&#x767D;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>TRIM([[BOTH | LEADING | TRAILING]</p>
        <p>&#x3000;&#x3000;[remstr] FROM] str)</p>
      </td>
      <td style="text-align:left">&#x53BB;&#x9664;&#x5B57;&#x4E32;&#x7D44;&#x4E8C;&#x908A;&#x7A7A;&#x767D;</td>
    </tr>
    <tr>
      <td style="text-align:left">STRCMP(expr1,expr2)</td>
      <td style="text-align:left">
        <p>expr1 = expr2 return 0</p>
        <p>expr1 &gt; expr2 return 1</p>
        <p>expr1 &lt; expr2 return -1</p>
      </td>
    </tr>
  </tbody>
</table>

### 字串函數範例

{% tabs %}
{% tab title="LPAD.RPAD補字" %}
範例一：\(p.87\)

* LPAD不滿10個字往左補字串
* RPAD不滿10個字往右補字串

`SELECT ename, sal, LPAD(sal,10,'#'), RPAD(sal,10,'#')  
FROM   emp;`

```text
+--------+---------+------------------+------------------+
| ename  | sal     | LPAD(sal,10,'#') | RPAD(sal,10,'#') |
+--------+---------+------------------+------------------+
| SMITH  |  800.00 | ####800.00       | 800.00####       |
| ALLEN  | 1600.00 | ###1600.00       | 1600.00###       |
| WARD   | 1250.00 | ###1250.00       | 1250.00###       |
| JONES  | 2975.00 | ###2975.00       | 2975.00###       |
| MARTIN | 1250.00 | ###1250.00       | 1250.00###       |
| BLAKE  | 2850.00 | ###2850.00       | 2850.00###       |
| CLARK  | 2450.00 | ###2450.00       | 2450.00###       |
| SCOTT  | 3000.00 | ###3000.00       | 3000.00###       |
| KING   | 5000.00 | ###5000.00       | 5000.00###       |
| TURNER | 1500.00 | ###1500.00       | 1500.00###       |
| ADAMS  | 1100.00 | ###1100.00       | 1100.00###       |
| JAMES  |  950.00 | ####950.00       | 950.00####       |
| FORD   | 3000.00 | ###3000.00       | 3000.00###       |
| MILLER | 1300.00 | ###1300.00       | 1300.00###       |
+--------+---------+------------------+------------------+
14 rows in set (0.01 sec)
```

```text
mysql> SELECT ename,sal,concat(job,' in department ',deptno) job_dep
    -> FROM   emp
    -> WHERE  substr(ename,1,1)='M';
+--------+---------+---------------------------+
| ename  | sal     | job_dep                   |
+--------+---------+---------------------------+
| MARTIN | 1250.00 | SALESMAN in department 30 |
| MILLER | 1300.00 | CLERK in department 10    |
+--------+---------+---------------------------+
2 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="REPEAT重複字元\(p.88\)" %}
範例二：REPEAT，每一個星號\[\*\]表示$100元\(p.88\)

`SELECT ename, sal, repeat('*',ROUND(sal/100,0))  
FROM emp   
WHERE deptno = 10;`

呈現如下

| ename | sal | reapeat\('\*',ROUND\(sal/100,0\)\) |
| :--- | :--- | :--- |
| CLARK | 2450.00 | \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\* |
| KING | 5000.00 | \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\* |
| MILLER | 1300.00 | \*\*\*\*\*\*\*\*\*\*\*\*\* |
{% endtab %}
{% endtabs %}



## 【數值函數】\(p.87\)

| 函數 | 功能 |
| :--- | :--- |
| **`ROUND(x,d)`** | 四捨五入 |
| TRUNCATE\(x,d\) | 無條件捨去 |
| MOD\(n,m\) | 取餘數\(n被除數，m除數\) |
| CEIL\(x\) | 不小於x的最小整數。例如4.2==&gt;5　（無條件進位） |
| FLOOR\(x\) | 不大於x的最大整數。例如4.2==&gt;4　（無條件捨去） |
| POWER\(x,y\) | x的y次方。 $$x^y$$  |
| SQRT\(x\) | x的平方根。 $$√x$$  |
| ABS\(x\) | 絕對值 |
| SIGN\(x\) | 正負數 |
| RAND\(\) \| RAND\(n\) | 亂數，\(\)0~1 |
| PI\(\) | 圓周率 |
| RADIANS\(x\) | 度數轉徑值 |
| DEGREES\(x\) | 徑值轉度數 |

### 數值函數範例

{% tabs %}
{% tab title="ROUND四捨五入\(p.88\)" %}
範例一：ROUND四捨五入\(每一個星號\[\*\]表示$100元\)

`SELECT ename, sal, repeat('*',ROUND(sal/100,0))  
FROM emp   
WHERE deptno = 10;`

```text
+--------+---------+----------------------------------------------------+
| ename  | sal     | repeat('*',ROUND(sal/100,0))                       |
+--------+---------+----------------------------------------------------+
| CLARK  | 2450.00 | *************************                          |
| KING   | 5000.00 | ************************************************** |
| MILLER | 1300.00 | *************                                      |
+--------+---------+----------------------------------------------------+
3 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="FLOOR不大於.RAND亂數\(p.88\)" %}
範例二：隨機加薪\(?\)

* FLOOR回傳不大於X的最小整數 例如4.2，會回傳4
* RAND\(\)，數值為0~1的隨機亂數

`SELECT ename, sal, sal+FLOOR(RAND()*1000)  
FROM emp  
WHERE deptno = 10;`

```text
+-------+---------+------------------------+
| ename | sal     | sal+floor(rand()*1000) |
+-------+---------+------------------------+
| SMITH |  800.00 |                   1536 |
| JONES | 2975.00 |                   3505 |
| SCOTT | 3000.00 |                   3440 |
| ADAMS | 1100.00 |                   1711 |
| FORD  | 3000.00 |                   3736 |
+-------+---------+------------------------+
5 rows in set (0.01 sec)
```
{% endtab %}
{% endtabs %}

## 【日期時間函數】\(p.88\)

| 函數 | 功能 |
| :--- | :--- |
| CURDATE\(\) | 現在日期 |
| CURTIME\(\) | 現在時間 |
| CURRENT\_TIMESTAMP\(\) | 現在日期與時間 |
| NOW\(\) | 現在日期與時間 |
| UTC\_DATE\(\) | 格林威治日期 |
| UTC\_TIME\(\) | 格林威治時間 |
| UTC\_TIMESTAMP\(\) | 格林威治日期與時間 |
| YEAR\(date\) | 指定日期的年份 |
| MONTH\(date\) | 指定日期的月份 |
| DAY\(date\) | 指定日期的日 |
| HOUR\(time\) | 指定日期的時 |
| MINUTE\(time\) | 指定日期的分 |
| SECOND\(time\) | 指定日期的秒 |
| TIME\(expr\) | 時間單位 |
| MICROSECOND\(expr\) | 指定日期的微秒 |
| EXTRACT\(type FROM date\) | 指定日期的單位 |
| DAYNAME\(date\) | 日期名稱 |
| MONTHNAME\(date\) | 月份名稱 |
| DAYOFWEEK\(date\) | 一週中的第幾天。1星期天7星期六 |
| DAYOFMONTH\(date\) | 月分中的第幾天 |
| DAYOFYEAR\(date\) | 一年中的第幾天 |
| WEEK\(date\[,mode\]\) | 傳回週數0~52 |
| WEEKDAY\(day\) | 傳回星期索引0星期一6星期天 |
| WEEKOFYEAR\(date\) | 一年中第幾週 |
| YEARWEEK\(date\[,start\]\) | Returns year and week |

{% tabs %}
{% tab title="計算\(p.90\)" %}
| 函數 | 功能 |
| :--- | :--- |
| **`DATEDIFF`**\(expr1,expr2\) | 兩個日期相減\(差幾天\) |
| **`ADDDATE`**\(date,**`INTERVAL`** expr type\) | 日期加法 |
| SUBDATE\(date,INTERVAL expr type\) | 日期減法 |
| ADDTIME\(expr1,expr2\) | 時間加法 |
| SUBTIME\(expr1,expr2\) | 時間減法 |
| TIMEDIFF\(expr1,expr2\) | 時間減法 |
| TIMESTAMP\(expr1,expr2\) | 時間加法 |
| TIMESTAMPADD\(interval, int\_expr,datetime\_expr\) | 時間加法 |
| TIMESTAMPDIFF\(interval, datetime\_expr1, datetime\_expr2\) | 時間減法 |
| PERIOD\_DIFF\(p1,p2\) | 月份\(年月-年月\) |
{% endtab %}

{% tab title="轉換\(p.91\)" %}
| 函數 | 功能 |
| :--- | :--- |
| DATE\(expr\) | 字串轉日期 |
| STR\_TO\_DATE\(str,format\) | 字串轉日期 |
| MAKEDATE\(year,dayofyear\) | 日期字串轉日期 |
| MAKETIME\(hour,minute,second\) | 時間字串轉時間 |
| DATE\_FORMAT\(date,format\) | 日期格式化轉字串 |
| TIME\_FORMAT\(time,format\) | 時間格式化轉字串 |
| TO\_DAYS\(date\) | 距起算日的總天數 |
| FROM\_DAYS\(N\) | 將總天數轉成某日期 |
| LAST\_DAY\(date\) | 指定日期月份的最後一天 |
| QUARTER\(date\) | 一年中的第幾季 |
| TIME\_TO\_SEC\(time\) | 換算成一天總秒數 |
| SEC\_TO\_TIME\(seconds\) | 總秒數換算成一天時間 |
{% endtab %}

{% tab title="格式化成字串\(p.92\)" %}
DATE\_FORMAT\(_expr_ , '_specifier_'\)

<table>
  <thead>
    <tr>
      <th style="text-align:left">specifier</th>
      <th style="text-align:left">&#x8AAA;&#x660E;</th>
      <th style="text-align:left">&#x4F8B;&#x5982;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">%a</td>
      <td style="text-align:left">&#x4E09;&#x5B57;&#x6BCD;&#x661F;&#x671F;</td>
      <td style="text-align:left">Mon, Tue Wed...</td>
    </tr>
    <tr>
      <td style="text-align:left">%b</td>
      <td style="text-align:left">&#x4E09;&#x5B57;&#x6BCD;&#x6708;&#x4EFD;</td>
      <td style="text-align:left">Jan,Feb,Mar...</td>
    </tr>
    <tr>
      <td style="text-align:left">%c</td>
      <td style="text-align:left">&#x6578;&#x5B57;&#x6708;&#x4EFD;</td>
      <td style="text-align:left">1,2,3...,12</td>
    </tr>
    <tr>
      <td style="text-align:left">%D</td>
      <td style="text-align:left">&#x82F1;&#x6587;&#x65E5;&#x671F;</td>
      <td style="text-align:left">1st,2nd...</td>
    </tr>
    <tr>
      <td style="text-align:left">%d</td>
      <td style="text-align:left">&#x6578;&#x5B57;&#x65E5;&#x671F;(0&#x88DC;&#x4F4D;)</td>
      <td style="text-align:left">00,01,02....,31</td>
    </tr>
    <tr>
      <td style="text-align:left">%e</td>
      <td style="text-align:left">&#x6578;&#x5B57;&#x65E5;&#x671F;</td>
      <td style="text-align:left">1,2,3,...,31</td>
    </tr>
    <tr>
      <td style="text-align:left">%f</td>
      <td style="text-align:left">&#x5FAE;&#x79D2;&#x7BC4;&#x570D;</td>
      <td style="text-align:left">000000..999999</td>
    </tr>
    <tr>
      <td style="text-align:left">%H</td>
      <td style="text-align:left">24&#x5C0F;&#x6642;(0&#x88DC;&#x4F4D;)</td>
      <td style="text-align:left">00..23</td>
    </tr>
    <tr>
      <td style="text-align:left">%h</td>
      <td style="text-align:left">12&#x5C0F;&#x6642;(0&#x88DC;&#x4F4D;)</td>
      <td style="text-align:left">01,02,...12</td>
    </tr>
    <tr>
      <td style="text-align:left">%I</td>
      <td style="text-align:left">&#x540C;&#x4E0A;</td>
      <td style="text-align:left">&#x540C;&#x4E0A;</td>
    </tr>
    <tr>
      <td style="text-align:left">%i</td>
      <td style="text-align:left">&#x5206;&#x9418;(0&#x88DC;&#x4F4D;)</td>
      <td style="text-align:left">00,01,...,59</td>
    </tr>
    <tr>
      <td style="text-align:left">%j</td>
      <td style="text-align:left">&#x5929;&#x6578;(0&#x88DC;&#x4F4D;)</td>
      <td style="text-align:left">001,002,003,...366</td>
    </tr>
    <tr>
      <td style="text-align:left">%k</td>
      <td style="text-align:left">24&#x5C0F;&#x6642;</td>
      <td style="text-align:left">0,1,2,...23</td>
    </tr>
    <tr>
      <td style="text-align:left">%l</td>
      <td style="text-align:left">12&#x5C0F;&#x6642;</td>
      <td style="text-align:left">1,2,...,12</td>
    </tr>
    <tr>
      <td style="text-align:left">%M</td>
      <td style="text-align:left">&#x6708;&#x4EFD;&#x5168;&#x540D;</td>
      <td style="text-align:left">January, February,...December</td>
    </tr>
    <tr>
      <td style="text-align:left">%m</td>
      <td style="text-align:left">&#x6578;&#x5B57;&#x6708;&#x4EFD;(0&#x88DC;&#x4F4D;)</td>
      <td style="text-align:left">01,02,...12</td>
    </tr>
    <tr>
      <td style="text-align:left">%p</td>
      <td style="text-align:left">AM &#x6216; PM</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">%r</td>
      <td style="text-align:left">12&#x5C0F;&#x6642;hh:mm:ss AM&#x6216;PM</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">%S</td>
      <td style="text-align:left">&#x6578;&#x5B57;&#x79D2;(0&#x88DC;&#x4F4D;)</td>
      <td style="text-align:left">00,01,...59</td>
    </tr>
    <tr>
      <td style="text-align:left">%s</td>
      <td style="text-align:left">&#x540C;&#x4E0A;</td>
      <td style="text-align:left">&#x540C;&#x4E0A;</td>
    </tr>
    <tr>
      <td style="text-align:left">%T</td>
      <td style="text-align:left">12&#x5C0F;&#x6642;hh:mm:ss</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">%U</td>
      <td style="text-align:left">
        <p>&#x6578;&#x5B57;&#x9031;(0&#x88DC;&#x4F4D;)</p>
        <p>&#x7B2C;&#x4E00;&#x5929;&#x662F;&#x661F;&#x671F;&#x5929;</p>
      </td>
      <td style="text-align:left">00,01,02...53</td>
    </tr>
    <tr>
      <td style="text-align:left">%u</td>
      <td style="text-align:left">
        <p>&#x6578;&#x5B57;&#x9031;(0&#x88DC;&#x4F4D;)</p>
        <p>&#x7B2C;&#x4E00;&#x5929;&#x662F;&#x661F;&#x671F;&#x4E00;</p>
      </td>
      <td style="text-align:left">00,01,02...53</td>
    </tr>
    <tr>
      <td style="text-align:left">%V</td>
      <td style="text-align:left">&#x540C;%U&#x4F7F;&#x7528;%X</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">%v</td>
      <td style="text-align:left">&#x540C;%u&#x4F7F;&#x7528;%x</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">%W</td>
      <td style="text-align:left">&#x9031;&#x5168;&#x540D;</td>
      <td style="text-align:left">Sunday,Monday,...,Saturday</td>
    </tr>
    <tr>
      <td style="text-align:left">%w</td>
      <td style="text-align:left">&#x6578;&#x5B57;&#x9031;</td>
      <td style="text-align:left">0=Sunday, 1=Monday...6=Saturday</td>
    </tr>
    <tr>
      <td style="text-align:left">%X</td>
      <td style="text-align:left">&#x8207;%V&#x76F8;&#x4F3C;</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">%x</td>
      <td style="text-align:left">&#x8207;%V&#x76F8;&#x4F3C;</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">%Y</td>
      <td style="text-align:left">&#x6578;&#x5B57;&#x5E74;&#xFF0C;&#x56DB;&#x78BC;</td>
      <td style="text-align:left">2010,2011,...</td>
    </tr>
    <tr>
      <td style="text-align:left">%y</td>
      <td style="text-align:left">&#x6578;&#x5B57;&#x5E74;&#xFF0C;&#x4E8C;&#x78BC;</td>
      <td style="text-align:left">10,11,12...</td>
    </tr>
    <tr>
      <td style="text-align:left">%%</td>
      <td style="text-align:left">&#x589E;&#x52A0;&#x300C;%&#x300D;</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>
{% endtab %}
{% endtabs %}



### 日期時間函數範例

{% tabs %}
{% tab title="當日CURDATE\(\)" %}
範例：當週當年當月第幾天\(p.89\)

`SELECT CURDATE() 當日   
,DAYOFWEEK(CURDATE()) '這週第幾天(1sunday 7Saturday)'   
,WEEKDAY(CURDATE()) '這週第幾天(0monday 6saturday)'   
,DAYOFMONTH(CURDATE()) '這個月第幾天'   
,DAYOFYEAR(CURDATE()) '當年第幾天';`

```text
+------------+-------------------------------+-------------------------------+--------------+------------+
| 當日        | 這週第幾天(1sunday 7Saturday)  | 這週第幾天(0monday 6saturday)   | 這個月第幾天   | 當年第幾天   |
+------------+-------------------------------+-------------------------------+--------------+------------+
| 2020-09-03 |                             5 |                             3 |            3 |        247 |
+------------+-------------------------------+-------------------------------+--------------+------------+
1 row in set (0.01 sec)
```
{% endtab %}

{% tab title="YEARWEEK\(\)" %}
範例：YEARWEEK當日是當年的第幾天\(p.89\)

`SELECT CURDATE(), YEARWEEK(CURDATE());`

```text
mysql> SELECT CURDATE(), YEARWEEK(CURDATE());
+------------+---------------------+
| CURDATE()  | YEARWEEK(CURDATE()) |
+------------+---------------------+
| 2020-09-03 |              202035 |-- 🔹2020年的第35週
+------------+---------------------+
1 row in set (0.00 sec)
```
{% endtab %}

{% tab title="查詢" %}
範例：查詢現在系統日期時間\(p.90\)

`SELECT NOW() '現在'   
　,DAYNAME(NOW()) '現在星期'   
　,EXTRACT(MONTH FROM CURDATE()) '現在幾月'   
　,DATEDIFF(CURDATE(),'20150317') '距離2015-03-17多久了';`

呈現效果如下

| 現在 | 現在星期 | 現在幾月 | 距離2015-03-17多久了 |
| :--- | :--- | :--- | :--- |
| 2020-06-24 11:45:11 | Wednesday | 6 | 1926 |
{% endtab %}

{% tab title="計算" %}
範例：日期時間計算\(p.90\)

`SELECT CURDATE() '當日'   
,ADDDATE(CURDATE(), INTERVAL 3 day) '加3天'   
,ADDDATE(CURDATE(), INTERVAL 3 MONTH) '加3月'   
,ADDDATE(CURDATE(), INTERVAL 3 YEAR) '加3年';`

```text
+------------+------------+------------+------------+
| 當日        | 加3天       | 加3月      | 加3年       |
+------------+------------+------------+------------+
| 2020-09-03 | 2020-09-06 | 2020-12-03 | 2023-09-03 |
+------------+------------+------------+------------+
1 row in set (0.00 sec)
```

```sql
-- 加六個月(p.91)
SELECT ename, hiredate, ADDDATE(hiredate, INTERVAL 6 Month)
FROM   emp;
/*
+--------+---------------------+-------------------------------------+
| ename  | hiredate            | ADDDATE(hiredate, INTERVAL 6 Month) |
+--------+---------------------+-------------------------------------+
| SMITH  | 1980-12-17 00:00:00 | 1981-06-17 00:00:00                 |
| ALLEN  | 1981-02-20 00:00:00 | 1981-08-20 00:00:00                 |
| WARD   | 1981-02-22 00:00:00 | 1981-08-22 00:00:00                 |
| JONES  | 1981-04-02 00:00:00 | 1981-10-02 00:00:00                 |
| MARTIN | 1981-09-28 00:00:00 | 1982-03-28 00:00:00                 |
| BLAKE  | 1981-05-01 00:00:00 | 1981-11-01 00:00:00                 |
| CLARK  | 1981-06-09 00:00:00 | 1981-12-09 00:00:00                 |
| SCOTT  | 1982-12-09 00:00:00 | 1983-06-09 00:00:00                 |
| KING   | 1981-11-17 00:00:00 | 1982-05-17 00:00:00                 |
| TURNER | 1981-09-08 00:00:00 | 1982-03-08 00:00:00                 |
| ADAMS  | 1983-01-12 00:00:00 | 1983-07-12 00:00:00                 |
| JAMES  | 1981-12-03 00:00:00 | 1982-06-03 00:00:00                 |
| FORD   | 1981-12-03 00:00:00 | 1982-06-03 00:00:00                 |
| MILLER | 1982-01-23 00:00:00 | 1982-07-23 00:00:00                 |
+--------+---------------------+-------------------------------------+
14 rows in set (0.00 sec)*/
```
{% endtab %}

{% tab title="格式化" %}
範例：將日期格式化\(p.93\)  
星期全名、日期三碼,月份全名,年分四碼

`SELECT CURDATE(), DATE_FORMAT(CURDATE(),'%W %D %M %Y');`

```text
+------------+--------------------------------------+
| CURDATE()  | DATE_FORMAT(CURDATE(),'%W %D %M %Y') |
+------------+--------------------------------------+
| 2020-09-03 | Thursday 3rd September 2020          |
+------------+--------------------------------------+
1 row in set (0.01 sec)
```

```text
mysql> SELECT CURDATE(),DATE_FORMAT(CURDATE(),' %W,the %D of %M, %Y');
+------------+-----------------------------------------------+
| CURDATE()  | DATE_FORMAT(CURDATE(),' %W,the %D of %M, %Y') |
+------------+-----------------------------------------------+
| 2020-09-03 |  Thursday,the 3rd of September, 2020          |
+------------+-----------------------------------------------+
1 row in set (0.00 sec)
```
{% endtab %}
{% endtabs %}



## 【資料型態轉換函數】\(p.93\)

* 函數
  * CAST\(expr AS type\)
  * **`CONVERT(expr, type)`**
* 資料型態type
  * BINARY
  * CHAR
  * DATE
  * DATETIME
  * SIGNED \[INTEGER\]
  * TIME
  * UNSIGNED \[INTEGER\]

### 資料型態轉換函數範例

{% tabs %}
{% tab title="CAST" %}
跟CONVERT寫法不同，但結果一樣\(p.94\)

`SELECT CAST(NOW() AS DATE) X1,   
CAST(CAST(1-2 AS UNSIGNED) AS SIGNED) X2,   
CAST(1-2 AS UNSIGNED) X3,   
CAST(1 AS UNSIGNED) - 2.0 X4;`

```text
+------------+----+----------------------+------+
| X1         | X2 | X3                   | X4   |
+------------+----+----------------------+------+
| 2020-09-03 | -1 | 18446744073709551615 | -1.0 |
+------------+----+----------------------+------+
1 row in set (0.01 sec)
```
{% endtab %}

{% tab title="CONVERT" %}
跟CAST寫法不同，但結果一樣\(p.94\)

`SELECT CONVERT(NOW(),DATE) X1,   
CONVERT(CONVERT(1-2,UNSIGNED),SIGNED) X2,   
CONVERT(1-2,UNSIGNED) X3,   
CONVERT(1,UNSIGNED)-2.0 X4;`

```text
+------------+----+----------------------+------+
| X1         | X2 | X3                   | X4   |
+------------+----+----------------------+------+
| 2020-09-03 | -1 | 18446744073709551615 | -1.0 |
+------------+----+----------------------+------+
1 row in set (0.00 sec)
```
{% endtab %}
{% endtabs %}

## 【通用函數】\(p.94\)

### 系統資訊函數\(p.94\)

| 函數 | 功能 |
| :--- | :--- |
| USER\(\) | 連線的使用者 |
| VERSION\(\) | 資料庫版本 |
| DATABASE\(\) | 連線的資料庫 |
| CONNECTION\_ID\(\) | 連線的connection ID |
| CHARSET\(str\) | 字串所屬的字元集 |

```text
mysql> SELECT USER(), VERSION(), DATABASE(),
    -> CONNECTION_ID(), CHARSET('abc');
+----------------+-----------+------------+-----------------+----------------+
| USER()         | VERSION() | DATABASE() | CONNECTION_ID() | CHARSET('abc') |
+----------------+-----------+------------+-----------------+----------------+
| root@localhost | 8.0.21    | demotest   |             443 | big5           |
+----------------+-----------+------------+-----------------+----------------+
1 row in set (0.00 sec)
```

### 流程控制函數\(p.95\)

| 函數 | 功能 |
| :--- | :--- |
| **`IFNULL(expr1,expr2)`** | IFNULL?expr1:expr2 |
| **`IF(expr1,expr2,expr3)`** | IF expr1?expr2:expr3 |
| NULLIF\(expr1,expr2\) | expr1==expr2?NULL:expr1 |

{% tabs %}
{% tab title="\(p.95\)IFNULL\(\)" %}
```text
-- (p.95)IFNULL(這個是空的嗎,是就做這個,不是就做這個)
mysql> SELECT IFNULL(1,0),
    ->        IFNULL(NULL,10),
    ->        IFNULL(1/0,10),
    ->        IFNULL(1/0,'yes');
+-------------+-----------------+----------------+-------------------+
| IFNULL(1,0) | IFNULL(NULL,10) | IFNULL(1/0,10) | IFNULL(1/0,'yes') |
+-------------+-----------------+----------------+-------------------+
|           1 |              10 |        10.0000 | yes               |
+-------------+-----------------+----------------+-------------------+
1 row in set (0.00 sec)
```
{% endtab %}

{% tab title="\(p.96\) IF\(\)" %}
```
-- IF(判斷,是就做這個,不是就做這個)
mysql> SELECT IF(1>2,2,3) x1,
    ->        IF(1<2,'yes','no') x2,
    ->        IF(STRCMP('test','test1'),'no','yes')x3;
+----+-----+----+
| x1 | x2  | x3 |
+----+-----+----+
|  3 | yes | no |
+----+-----+----+
1 row in set (0.00 sec)
```
{% endtab %}

{% tab title="\(p.96\) NULLIF\(\)" %}
```
-- NULLIF(敘述1,敘述2) 若敘述1與敘述2相等就執行NULL，不相等就執行敘述1
mysql> SELECT NULLIF(1,1) ,NULLIF(1,0),NULLIF(0,1);
+-------------+-------------+-------------+
| NULLIF(1,1) | NULLIF(1,0) | NULLIF(0,1) |
+-------------+-------------+-------------+
|        NULL |           1 |           0 |
+-------------+-------------+-------------+
1 row in set (0.01 sec)
```
{% endtab %}
{% endtabs %}

## 作業練習－DQL資料型態\(p.97\)

1. 顯示系統目前的日期並將 表頭命名為「系統日期」
2. 顯示所有員工之員編、姓名、薪資、薪資+15%，並以整數表示，表頭命名為new salary。
3. 接上題，增加一個資料向表頭命名為increase\(new salary 扣除salary的值\)
4. 🟡顯示員工姓名、到職日、檢討薪資日期（到職日六月後的第一個星期一），該欄位命名為review， 自訂日期格式為：Sunday, the seventh of September。
5. 顯示每位員工的姓名、資料項\(months\_worked\)：計算到今天為止工作了幾個月\(月數四捨五入到整數\)
6. 顯示格式：&lt;員工姓名&gt; earns &lt;薪水&gt; monthly but wants &lt;3倍薪水&gt;.並將表頭命名為dream salaries。
7. 顯示所有員工之姓名和薪資，設定薪資長度為15字元並在左邊加上$符號，表頭命名為SALARY。
8. 顯示員工姓名、到職日，資料項\(DAY\)： 顯示員工被雇用那天為星期幾，並以星期一作為一周的起始日，依星期排序。
9. 顯示員工姓名和名為comm欄位：顯示佣金額，若該員工沒有佣金則顯示"NO COMMISSION"
10. 顯示資料項employee\_and\_their\_salaries的資料來顯示所有員工姓名、薪資， 且用星號表示他們的薪資，每一個星號表100元，薪資由高至低顯示。

{% tabs %}
{% tab title="1" %}
```text
-- 顯示系統目前的日期並將 表頭命名為「系統日期」
SELECT CURDATE() '系統日期';
+------------+
| 系統日期    |
+------------+
| 2020-07-01 |
+------------+
1 row in set (0.14 sec)
```
{% endtab %}

{% tab title="2" %}
```
-- 顯示所有員工之員編、姓名、薪資、薪資+15%，並以整數表示，表頭命名為new salary。
SELECT empno, ename, sal, round(sal*1.15,2) 'New Salary' 
	FROM emp;
+-------+--------+---------+------------+
| empno | ename  | sal     | New Salary |
+-------+--------+---------+------------+
|  7369 | SMITH  |  800.00 |     920.00 |
|  7499 | ALLEN  | 1600.00 |    1840.00 |
|  7521 | WARD   | 1250.00 |    1437.50 |
|  7566 | JONES  | 2975.00 |    3421.25 |
|  7654 | MARTIN | 1250.00 |    1437.50 |
|  7698 | BLAKE  | 2850.00 |    3277.50 |
|  7782 | CLARK  | 2450.00 |    2817.50 |
|  7788 | SCOTT  | 3000.00 |    3450.00 |
|  7839 | KING   | 5000.00 |    5750.00 |
|  7844 | TURNER | 1500.00 |    1725.00 |
|  7876 | ADAMS  | 1100.00 |    1265.00 |
|  7900 | JAMES  |  950.00 |    1092.50 |
|  7902 | FORD   | 3000.00 |    3450.00 |
|  7934 | MILLER | 1300.00 |    1495.00 |
+-------+--------+---------+------------+
14 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="3" %}
```
-- 接上題，增加一個資料向表頭命名為increase(new salary 扣除salary的值)

SELECT empno, 
	ename, 
	sal, 
	round(sal*1.15,2) 'New Salary', 
	round(sal*0.15,2) 'Increase' 
FROM emp;
+-------+--------+---------+------------+----------+
| empno | ename  | sal     | New Salary | Increase |
+-------+--------+---------+------------+----------+
|  7369 | SMITH  |  800.00 |     920.00 |   120.00 |
|  7499 | ALLEN  | 1600.00 |    1840.00 |   240.00 |
|  7521 | WARD   | 1250.00 |    1437.50 |   187.50 |
|  7566 | JONES  | 2975.00 |    3421.25 |   446.25 |
|  7654 | MARTIN | 1250.00 |    1437.50 |   187.50 |
|  7698 | BLAKE  | 2850.00 |    3277.50 |   427.50 |
|  7782 | CLARK  | 2450.00 |    2817.50 |   367.50 |
|  7788 | SCOTT  | 3000.00 |    3450.00 |   450.00 |
|  7839 | KING   | 5000.00 |    5750.00 |   750.00 |
|  7844 | TURNER | 1500.00 |    1725.00 |   225.00 |
|  7876 | ADAMS  | 1100.00 |    1265.00 |   165.00 |
|  7900 | JAMES  |  950.00 |    1092.50 |   142.50 |
|  7902 | FORD   | 3000.00 |    3450.00 |   450.00 |
|  7934 | MILLER | 1300.00 |    1495.00 |   195.00 |
+-------+--------+---------+------------+----------+
14 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="🟡4" %}
```
/*顯示員工姓名、到職日、檢討薪資日期（到職日六月後的第一個星期一），該欄位命名為review，
自訂日期格式為：Sunday, the seventh of September。*/
SELECT ename, 
hiredate, 
	DATE_FORMAT(ADDDATE(ADDDATE(hiredate,INTERVAL 6 MONTH), 
		INTERVAL MOD(7-WEEKDAY(ADDDATE(hiredate,INTERVAL 6 MONTH)),7) DAY)
	, '%W ,the %D of %M') 'REVIEW' 
	FROM emp;
+--------+---------------------+------------------------------+
| ename  | hiredate            | REVIEW                       |
+--------+---------------------+------------------------------+
| SMITH  | 1980-12-17 00:00:00 | Monday ,the 22nd of June     |
| ALLEN  | 1981-02-20 00:00:00 | Monday ,the 24th of August   |
| WARD   | 1981-02-22 00:00:00 | Monday ,the 24th of August   |
| JONES  | 1981-04-02 00:00:00 | Monday ,the 5th of October   |
| MARTIN | 1981-09-28 00:00:00 | Monday ,the 29th of March    |
| BLAKE  | 1981-05-01 00:00:00 | Monday ,the 2nd of November  |
| CLARK  | 1981-06-09 00:00:00 | Monday ,the 14th of December |
| SCOTT  | 1982-12-09 00:00:00 | Monday ,the 13th of June     |
| KING   | 1981-11-17 00:00:00 | Monday ,the 17th of May      |
| TURNER | 1981-09-08 00:00:00 | Monday ,the 8th of March     |
| ADAMS  | 1983-01-12 00:00:00 | Monday ,the 18th of July     |
| JAMES  | 1981-12-03 00:00:00 | Monday ,the 7th of June      |
| FORD   | 1981-12-03 00:00:00 | Monday ,the 7th of June      |
| MILLER | 1982-01-23 00:00:00 | Monday ,the 26th of July     |
+--------+---------------------+------------------------------+
14 rows in set (0.02 sec)

↓自我流的解釋XD：
設 x = +6MONTH
			  +month						+weekday
adddate ( x INTERVAL +MOD(7-week(x)) DAY )
```
{% endtab %}

{% tab title="5" %}
```
-- 顯示每位員工的姓名、資料項(months_worked)：計算到今天為止工作了幾個月(月數四捨五入到整數)
SELECT ename, ROUND(DATEDIFF(curdate(), hiredate)/365*12,0) 'MONTHS_WORKED' 
	FROM emp;
+--------+---------------+
| ename  | MONTHS_WORKED |
+--------+---------------+
| SMITH  |           475 |
| ALLEN  |           473 |
| WARD   |           473 |
| JONES  |           471 |
| MARTIN |           465 |
| BLAKE  |           470 |
| CLARK  |           469 |
| SCOTT  |           451 |
| KING   |           464 |
| TURNER |           466 |
| ADAMS  |           450 |
| JAMES  |           463 |
| FORD   |           463 |
| MILLER |           462 |
+--------+---------------+
14 rows in set (0.02 sec)
```
{% endtab %}

{% tab title="6" %}
```
/*顯示格式：<員工姓名> earns <薪水> monthly but wants <3倍薪水>.
  並將表頭命名為dream salaries。
*/
SELECT CONCAT(ename, ' earns ', sal ,' monthly but wants ' ,3*sal) 
							'Dream Salaries' 
	FROM emp;
+------------------------------------------------+
| Dream Salaries                                 |
+------------------------------------------------+
| SMITH earns 800.00 monthly but wants 2400.00   |
| ALLEN earns 1600.00 monthly but wants 4800.00  |
| WARD earns 1250.00 monthly but wants 3750.00   |
| JONES earns 2975.00 monthly but wants 8925.00  |
| MARTIN earns 1250.00 monthly but wants 3750.00 |
| BLAKE earns 2850.00 monthly but wants 8550.00  |
| CLARK earns 2450.00 monthly but wants 7350.00  |
| SCOTT earns 3000.00 monthly but wants 9000.00  |
| KING earns 5000.00 monthly but wants 15000.00  |
| TURNER earns 1500.00 monthly but wants 4500.00 |
| ADAMS earns 1100.00 monthly but wants 3300.00  |
| JAMES earns 950.00 monthly but wants 2850.00   |
| FORD earns 3000.00 monthly but wants 9000.00   |
| MILLER earns 1300.00 monthly but wants 3900.00 |
+------------------------------------------------+
14 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="7" %}
```
-- 顯示所有員工之姓名和薪資，設定薪資長度為15字元並在左邊加上$符號，表頭命名為SALARY。
SELECT ename, lpad(sal,15,'$') 'Salary' 
	FROM emp;
+--------+-----------------+
| ename  | Salary          |
+--------+-----------------+
| SMITH  | $$$$$$$$$800.00 |
| ALLEN  | $$$$$$$$1600.00 |
| WARD   | $$$$$$$$1250.00 |
| JONES  | $$$$$$$$2975.00 |
| MARTIN | $$$$$$$$1250.00 |
| BLAKE  | $$$$$$$$2850.00 |
| CLARK  | $$$$$$$$2450.00 |
| SCOTT  | $$$$$$$$3000.00 |
| KING   | $$$$$$$$5000.00 |
| TURNER | $$$$$$$$1500.00 |
| ADAMS  | $$$$$$$$1100.00 |
| JAMES  | $$$$$$$$$950.00 |
| FORD   | $$$$$$$$3000.00 |
| MILLER | $$$$$$$$1300.00 |
+--------+-----------------+
14 rows in set (0.05 sec)
```
{% endtab %}

{% tab title="8" %}
```
/*顯示員工姓名、到職日，資料項(DAY)：
顯示員工被雇用那天為星期幾，並以星期一作為一周的起始日，依星期排序。*/

SELECT ename, hiredate, weekday(hiredate)+1 'Day' 
	FROM emp
    order by 3;
+--------+---------------------+------+
| ename  | hiredate            | Day  |
+--------+---------------------+------+
| MARTIN | 1981-09-28 00:00:00 |    1 |
| CLARK  | 1981-06-09 00:00:00 |    2 |
| KING   | 1981-11-17 00:00:00 |    2 |
| TURNER | 1981-09-08 00:00:00 |    2 |
| SMITH  | 1980-12-17 00:00:00 |    3 |
| ADAMS  | 1983-01-12 00:00:00 |    3 |
| JONES  | 1981-04-02 00:00:00 |    4 |
| SCOTT  | 1982-12-09 00:00:00 |    4 |
| JAMES  | 1981-12-03 00:00:00 |    4 |
| FORD   | 1981-12-03 00:00:00 |    4 |
| ALLEN  | 1981-02-20 00:00:00 |    5 |
| BLAKE  | 1981-05-01 00:00:00 |    5 |
| MILLER | 1982-01-23 00:00:00 |    6 |
| WARD   | 1981-02-22 00:00:00 |    7 |
+--------+---------------------+------+
14 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="9" %}
```
-- 顯示員工姓名和名為comm欄位：顯示佣金額，若該員工沒有佣金則顯示"NO COMMISSION"
SELECT ename, ifnull(comm,'No Commission.') 'Comm' 
	FROM emp;
+--------+----------------+
| ename  | Comm           |
+--------+----------------+
| SMITH  | No Commission. |
| ALLEN  | 300.00         |
| WARD   | 500.00         |
| JONES  | No Commission. |
| MARTIN | 1400.00        |
| BLAKE  | No Commission. |
| CLARK  | No Commission. |
| SCOTT  | No Commission. |
| KING   | No Commission. |
| TURNER | 0.00           |
| ADAMS  | No Commission. |
| JAMES  | No Commission. |
| FORD   | No Commission. |
| MILLER | No Commission. |
+--------+----------------+
14 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="10" %}
```
/*顯示資料項employee_and_their_salaries的資料來顯示所有員工姓名、薪資，
且用星號表示他們的薪資，每一個星號表100元，薪資由高至低顯示。
*/

SELECT CONCAT(ename, ' ' ,REPEAT('*',TRUNCATE(sal/100,0))) 
             'EMPLOYEE_AND_THEIR_SALARIES' 
FROM emp 
ORDER BY sal DESC;
+---------------------------------------------------------+
| EMPLOYEE_AND_THEIR_SALARIES                             |
+---------------------------------------------------------+
| KING ************************************************** |
| SCOTT ******************************                    |
| FORD ******************************                     |
| JONES *****************************                     |
| BLAKE ****************************                      |
| CLARK ************************                          |
| ALLEN ****************                                  |
| TURNER ***************                                  |
| MILLER *************                                    |
| WARD ************                                       |
| MARTIN ************                                     |
| ADAMS ***********                                       |
| JAMES *********                                         |
| SMITH ********                                          |
+---------------------------------------------------------+
14 rows in set (0.02 sec)
```
{% endtab %}
{% endtabs %}

