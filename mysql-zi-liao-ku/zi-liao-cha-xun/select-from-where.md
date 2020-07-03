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

## 作業練習－DQL-SELECT

1. 建立一個查詢來顯示部門\(dept\)資料表中的所有資料。
2. 建立一個查詢來顯示每一位員工的姓名\(name\)、職稱\(job\)、到職日\(hire date\)、員工編號\(employee number\)，並將員工編號顯示在最前面。
3. 建立一個查詢來顯示所有員工所擔任的職稱有哪些\(重複資料只顯示一次\)。
4. 建立一個查詢來顯示每一位員工的姓名、職稱、到職日、員編，並將員編顯示在最前面。 將資料表頭重新命名:emp\#,Employee,job,hire date。
5. 建立一個查詢將姓名、職稱串接為一個資料項\(資料中間利用一個空白和一個逗號做區隔\)，將表頭重新命名為employee and title。

{% tabs %}
{% tab title="1" %}
```text
-- 建立一個查詢來顯示部門(dept)資料表中的所有資料。
SELECT * 
	FROM dept;
+--------+------------+----------+
| DEPTNO | DNAME      | LOC      |
+--------+------------+----------+
|     10 | ACCOUNTING | NEW YORK |
|     20 | RESEARCH   | DALLAS   |
|     30 | SALES      | CHICAGO  |
|     40 | OPERATIONS | BOSTON   |
+--------+------------+----------+
4 rows in set (0.00 sec)	
```
{% endtab %}

{% tab title="2" %}
```
/*建立一個查詢來顯示每一位員工的
姓名(name)、職稱(job)、到職日(hire date)、員工編號(employee number)，
並將員工編號顯示在最前面。
*/
SELECT empno, ename, job, hiredate 
	FROM emp;
+-------+--------+-----------+---------------------+
| empno | ename  | job       | hiredate            |
+-------+--------+-----------+---------------------+
|  7369 | SMITH  | CLERK     | 1980-12-17 00:00:00 |
|  7499 | ALLEN  | SALESMAN  | 1981-02-20 00:00:00 |
|  7521 | WARD   | SALESMAN  | 1981-02-22 00:00:00 |
|  7566 | JONES  | MANAGER   | 1981-04-02 00:00:00 |
|  7654 | MARTIN | SALESMAN  | 1981-09-28 00:00:00 |
|  7698 | BLAKE  | MANAGER   | 1981-05-01 00:00:00 |
|  7782 | CLARK  | MANAGER   | 1981-06-09 00:00:00 |
|  7788 | SCOTT  | ANALYST   | 1982-12-09 00:00:00 |
|  7839 | KING   | PRESIDENT | 1981-11-17 00:00:00 |
|  7844 | TURNER | SALESMAN  | 1981-09-08 00:00:00 |
|  7876 | ADAMS  | CLERK     | 1983-01-12 00:00:00 |
|  7900 | JAMES  | CLERK     | 1981-12-03 00:00:00 |
|  7902 | FORD   | ANALYST   | 1981-12-03 00:00:00 |
|  7934 | MILLER | CLERK     | 1982-01-23 00:00:00 |
+-------+--------+-----------+---------------------+
14 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="3" %}
```
-- 建立一個查詢來顯示所有員工所擔任的職稱有哪些(重複資料只顯示一次)。
SELECT DISTINCT job 
	FROM emp;
+-----------+
| job       |
+-----------+
| CLERK     |
| SALESMAN  |
| MANAGER   |
| ANALYST   |
| PRESIDENT |
+-----------+
5 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="4" %}
```
/*建立一個查詢來顯示每一位員工的姓名、職稱、到職日、員編，並將員編顯示在最前面。
將資料表頭重新命名:emp#,Employee,job,hire date。
*/
SELECT empno 'Emp#', ename 'Employee', job 'Job', hiredate 'Hire Date' 
	FROM emp;
+------+----------+-----------+---------------------+
| Emp# | Employee | Job       | Hire Date           |
+------+----------+-----------+---------------------+
| 7369 | SMITH    | CLERK     | 1980-12-17 00:00:00 |
| 7499 | ALLEN    | SALESMAN  | 1981-02-20 00:00:00 |
| 7521 | WARD     | SALESMAN  | 1981-02-22 00:00:00 |
| 7566 | JONES    | MANAGER   | 1981-04-02 00:00:00 |
| 7654 | MARTIN   | SALESMAN  | 1981-09-28 00:00:00 |
| 7698 | BLAKE    | MANAGER   | 1981-05-01 00:00:00 |
| 7782 | CLARK    | MANAGER   | 1981-06-09 00:00:00 |
| 7788 | SCOTT    | ANALYST   | 1982-12-09 00:00:00 |
| 7839 | KING     | PRESIDENT | 1981-11-17 00:00:00 |
| 7844 | TURNER   | SALESMAN  | 1981-09-08 00:00:00 |
| 7876 | ADAMS    | CLERK     | 1983-01-12 00:00:00 |
| 7900 | JAMES    | CLERK     | 1981-12-03 00:00:00 |
| 7902 | FORD     | ANALYST   | 1981-12-03 00:00:00 |
| 7934 | MILLER   | CLERK     | 1982-01-23 00:00:00 |
+------+----------+-----------+---------------------+
14 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="5" %}
```
/*建立一個查詢將姓名、職稱串接為一個資料項(資料中間利用一個空白和一個逗號做區隔)，
將表頭重新命名為employee and title。
*/
SELECT CONCAT(ename,', ',job) 'Employee and Title' 
	FROM emp;
+--------------------+
| Employee and Title |
+--------------------+
| SMITH, CLERK       |
| ALLEN, SALESMAN    |
| WARD, SALESMAN     |
| JONES, MANAGER     |
| MARTIN, SALESMAN   |
| BLAKE, MANAGER     |
| CLARK, MANAGER     |
| SCOTT, ANALYST     |
| KING, PRESIDENT    |
| TURNER, SALESMAN   |
| ADAMS, CLERK       |
| JAMES, CLERK       |
| FORD, ANALYST      |
| MILLER, CLERK      |
+--------------------+
14 rows in set (0.00 sec)
```
{% endtab %}
{% endtabs %}



## 作業練習－DQL-WHERE

1. 顯示出所有員工薪資超過2850元的員工姓名和薪資。
2. 顯示員編7566員工姓名及其所屬部門。
3. 顯示薪資不介於1500~2850元的員工姓名及薪資。
4. 顯示於1981-2-20和1981-5-1間進入公司的員工姓名、職稱、到職日，並依到職日由小到大排序。
5. 顯示部門10和30所有員工姓名及其所屬部門編號，依名字英文字母排序。
6. 顯示薪資超過1500且在10或30部門工作員工之姓名和薪資， 表頭命名為employee和monthly salary。
7. 顯示於1982年進公司的所有員工姓名、職稱、到職日。
8. 顯示沒有主管的員工姓名和職稱。
9. 顯示所有有賺取佣金的員工姓名、薪資、佣金，並依薪資和佣金做降冪排序。
10. 顯示所有名字裡第三個英文字母為A的員工之姓名與職稱
11. 顯示名字裡有兩個L且在30部門工作或津里是7782的員工姓名、經理員編及其所屬部門編號。
12. 顯示值稱為Clerk或analyst且薪水不等於1000,3000,5000的員工姓名、職稱、薪資。
13. 顯示佣金比薪水的1.1倍還多的員工姓名、薪資、佣金。

{% tabs %}
{% tab title="1" %}
```text
-- 顯示出所有員工薪資超過2850元的員工姓名和薪資。
SELECT ename, sal 
	FROM emp 
  WHERE sal>2850;
 +-------+---------+
| ename | sal     |
+-------+---------+
| JONES | 2975.00 |
| SCOTT | 3000.00 |
| KING  | 5000.00 |
| FORD  | 3000.00 |
+-------+---------+
4 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="2" %}
```
-- 顯示員編7566員工姓名及其所屬部門。
SELECT ename, deptno 
	FROM emp 
  WHERE empno='7566';
+-------+--------+
| ename | deptno |
+-------+--------+
| JONES |     20 |
+-------+--------+
1 row in set (0.00 sec)
```
{% endtab %}

{% tab title="3" %}
```
-- 顯示薪資不介於1500~2850元的員工姓名及薪資。

SELECT ename, sal 
	FROM emp 
  WHERE sal NOT BETWEEN 1500 AND 2850;
+--------+---------+
| ename  | sal     |
+--------+---------+
| SMITH  |  800.00 |
| WARD   | 1250.00 |
| JONES  | 2975.00 |
| MARTIN | 1250.00 |
| SCOTT  | 3000.00 |
| KING   | 5000.00 |
| ADAMS  | 1100.00 |
| JAMES  |  950.00 |
| FORD   | 3000.00 |
| MILLER | 1300.00 |
+--------+---------+
10 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="4" %}
```
-- 顯示於1981-2-20和1981-5-1間進入公司的員工姓名、職稱、到職日，並依到職日由小到大排序。
SELECT ename, job, hiredate 
	FROM emp 
  WHERE hiredate BETWEEN '1981-2-20' AND '1981-5-1' 
  ORDER BY hiredate;
+-------+----------+---------------------+
| ename | job      | hiredate            |
+-------+----------+---------------------+
| ALLEN | SALESMAN | 1981-02-20 00:00:00 |
| WARD  | SALESMAN | 1981-02-22 00:00:00 |
| JONES | MANAGER  | 1981-04-02 00:00:00 |
| BLAKE | MANAGER  | 1981-05-01 00:00:00 |
+-------+----------+---------------------+
4 rows in set (0.00 sec) 
```
{% endtab %}

{% tab title="5" %}
```
-- 顯示部門10和30所有員工姓名及其所屬部門編號，依名字英文字母排序。
SELECT ename, deptno 
	FROM emp 
  WHERE deptno IN (10,20) 
  ORDER BY ename;
+--------+--------+
| ename  | deptno |
+--------+--------+
| ADAMS  |     20 |
| CLARK  |     10 |
| FORD   |     20 |
| JONES  |     20 |
| KING   |     10 |
| MILLER |     10 |
| SCOTT  |     20 |
| SMITH  |     20 |
+--------+--------+
8 rows in set (0.02 sec) 
```
{% endtab %}

{% tab title="6" %}
```
/*顯示薪資超過1500且在10或30部門工作員工之姓名和薪資，
表頭命名為employee和monthly salary。
*/
SELECT ename 'Employee' ,sal 'Monthly Salary' 
	FROM emp 
  WHERE sal>1500 AND deptno IN (10,30);
+----------+----------------+
| Employee | Monthly Salary |
+----------+----------------+
| CLARK    |        2450.00 |
| KING     |        5000.00 |
| ALLEN    |        1600.00 |
| BLAKE    |        2850.00 |
+----------+----------------+
4 rows in set (0.00 sec)  
```
{% endtab %}

{% tab title="7" %}
```
-- 顯示於1982年進公司的所有員工姓名、職稱、到職日。
SELECT ename, job, hiredate
	FROM emp 
  WHERE hiredate BETWEEN '1982-01-01' AND '1982-12-31';
+--------+---------+---------------------+
| ename  | job     | hiredate            |
+--------+---------+---------------------+
| SCOTT  | ANALYST | 1982-12-09 00:00:00 |
| MILLER | CLERK   | 1982-01-23 00:00:00 |
+--------+---------+---------------------+
2 rows in set (0.00 sec)  
```
{% endtab %}

{% tab title="8" %}
```
-- 顯示沒有主管的員工姓名和職稱。
SELECT ename, job 
	FROM emp 
    WHERE mgr IS NULL;
+-------+-----------+
| ename | job       |
+-------+-----------+
| KING  | PRESIDENT |
+-------+-----------+
1 row in set (0.00 sec)    
```
{% endtab %}

{% tab title="9" %}
```
-- 顯示所有有賺取佣金的員工姓名、薪資、佣金，並依薪資和佣金做降冪排序。
SELECT ename, sal, comm 
	FROM emp 
    WHERE comm IS NOT NULL AND comm<>0 
    ORDER BY sal DESC, comm DESC;
+--------+---------+---------+
| ename  | sal     | comm    |
+--------+---------+---------+
| ALLEN  | 1600.00 |  300.00 |
| MARTIN | 1250.00 | 1400.00 |
| WARD   | 1250.00 |  500.00 |
+--------+---------+---------+
3 rows in set (0.00 sec)    
```
{% endtab %}

{% tab title="10" %}
```
-- 顯示所有名字裡第三個英文字母為A的員工之姓名與職稱
SELECT ename, job 
	FROM emp 
    WHERE ename LIKE '__A%';
+-------+---------+
| ename | job     |
+-------+---------+
| BLAKE | MANAGER |
| CLARK | MANAGER |
| ADAMS | CLERK   |
+-------+---------+
3 rows in set (0.00 sec)    
```
{% endtab %}

{% tab title="11" %}
```
-- 顯示名字裡有兩個L且在30部門工作或津里是7782的員工姓名、經理員編及其所屬部門編號。
SELECT ename, mgr, deptno 
	FROM emp 
    WHERE (ename LIKE '%LL%' AND deptno=30) OR (mgr='7782');
+--------+------+--------+
| ename  | mgr  | deptno |
+--------+------+--------+
| ALLEN  | 7698 |     30 |
| MILLER | 7782 |     10 |
+--------+------+--------+
2 rows in set (0.02 sec)
```
{% endtab %}

{% tab title="12" %}
```
-- 顯示值稱為Clerk或analyst且薪水不等於1000,3000,5000的員工姓名、職稱、薪資。
SELECT ename, job, sal 
	FROM emp 
    WHERE job IN ('Clerk','Analyst') AND sal NOT IN (1000,3000,5000);
+--------+-------+---------+
| ename  | job   | sal     |
+--------+-------+---------+
| SMITH  | CLERK |  800.00 |
| ADAMS  | CLERK | 1100.00 |
| JAMES  | CLERK |  950.00 |
| MILLER | CLERK | 1300.00 |
+--------+-------+---------+
4 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="13" %}
```
-- 顯示佣金比薪水的1.1倍還多的員工姓名、薪資、佣金。
SELECT ename, sal, comm 
	FROM emp 
    WHERE comm>sal*1.1;
+--------+---------+---------+
| ename  | sal     | comm    |
+--------+---------+---------+
| MARTIN | 1250.00 | 1400.00 |
+--------+---------+---------+
1 row in set (0.00 sec)
```
{% endtab %}
{% endtabs %}

