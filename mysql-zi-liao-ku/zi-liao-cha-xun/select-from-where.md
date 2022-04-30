---
description: 參照講義p.39~p.50、p.51~p.74
---

# SELECT FROM WHERE

## SELECT FROM(p.39)

* 顯示表格全部欄位及資料。\
  `SELECT * FROM` 表格名稱;\

* 顯示指定欄位及其底下的資料。\
  SELECT 欄位名稱1,欄位名稱2,欄位名稱3...\
  FROM 表格名稱;\

* 設定欄位名稱別名，以逗號區隔欄位。\
  SELECT 欄位名稱1 欄位別名1,欄位名稱2 欄位別名2,欄位名稱3 欄位別名3...\
  FROM 表格名稱;\

* 欄位合併 (p.47)\
  SELECT `concat`(欄位名稱1,’用甚麼連結(這是選填)’,欄位名稱2) 合併後的欄位名稱\
  FROM 表格名稱;\

* 重複資料列排除(DISTINCT)，例如想知道公司的部門有哪些，用員工資料查詢。 (p.48)\
  SELECT `DISTINCT` 欄位名稱\
  FROM 表格名稱;\

* 查詢結果傳回資料筆數(LIMIT) (p.49)\
  SELECT 欄位名稱1,欄位名稱2,欄位名稱3...\
  FROM 表格名稱\
  `LIMIT` \[(選填)跳過開始的?筆資料,] 顯示?筆資料;



## SELECT FROM WHERE(p.51)

* 特定運算子:

|     | BETWEEN _x1_ AND _x2_                                        | IN(_x1,x2,...,xn_)                                         | LIKE                                                                                                                                                                                                                              | IS NULL |
| --- | ------------------------------------------------------------ | ---------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- |
| 解說  | <p>在某範圍(x1~x2)內</p><p>例如1000~3000</p><p>包含x1和x2的值</p>        | <p>在某個列舉的集合中(IN的括號內的數)<br></p><p>x1或x2...或xn</p>           | <p>模糊比對</p><p>‘%x’任意長度字元</p><p>‘_x’一個字元</p>                                                                                                                                                                                       |         |
| 範例  | `WHERE`` `_`sal`_` ``BETWEEN`` `_`2000`_` ``AND`` `_`3500;`_ | `WHERE`` `_`code`_` ``IN (`_`'A'`_`,`_`'B'`_`,'`_`C'`_`);` | <p><code>WHERE </code><em><code>ename</code></em><code> LIKE </code><em><code>'_A%';</code></em></p><p>意思是第二個字是A，%表*任意字</p>                                                                                                       |         |
| 範例二 |                                                              |                                                            | <p><code>WHERE </code><em><code>content</code></em><code> LIKE </code><em><code>'%3\%%'</code></em><code> </code><strong><code>ESCAPE</code></strong><code> </code><em><code>'\'</code></em><code>;</code></p><p>跳脫字元「\」-- 3%</p> |         |

{% tabs %}
{% tab title="比較運算" %}
(p.53)

```sql
SELECT empno, ename,job,sal
FROM emp
WHERE sal >=3000;
/*
+-------+-------+-----------+---------+
| empno | ename | job       | sal     |
+-------+-------+-----------+---------+
|  7788 | SCOTT | ANALYST   | 3000.00 |
|  7839 | KING  | PRESIDENT | 5000.00 |
|  7902 | mary  | ANALYST   | 3000.00 |
+-------+-------+-----------+---------+
3 rows in set (0.02 sec)*/
```

(p.54)

```sql
SELECT ename,ename,job,deptno,hiredate,sal
FROM emp
WHERE ename = 'KING';
/*
+-------+-------+-----------+--------+---------------------+---------+
| ename | ename | job       | deptno | hiredate            | sal     |
+-------+-------+-----------+--------+---------------------+---------+
| KING  | KING  | PRESIDENT |     10 | 1981-11-17 00:00:00 | 5000.00 |
+-------+-------+-----------+--------+---------------------+---------+
1 row in set (0.00 sec)*/
```

```
mysql> SELECT ename, sal, comm
    -> FROM   emp
    -> WHERE  sal<=comm;
+--------+---------+---------+
| ename  | sal     | comm    |
+--------+---------+---------+
| MARTIN | 1250.00 | 1400.00 |
+--------+---------+---------+
1 row in set (0.00 sec)
```
{% endtab %}

{% tab title="邏輯運算" %}
(p.55) AND

```
SELECT empno,ename,job,sal
FROM   emp
WHERE  sal>=1100 AND job='clerk';
/*
+-------+--------+-------+---------+
| empno | ename  | job   | sal     |
+-------+--------+-------+---------+
|  7876 | ADAMS  | CLERK | 1100.00 |
|  7934 | MILLER | CLERK | 1300.00 |
+-------+--------+-------+---------+
2 rows in set (0.00 sec)*/
```

```
mysql> SELECT empno,ename,job,sal,mgr
    -> FROM   emp
    -> WHERE  sal>2000 AND job = 'manager';
+-------+-------+---------+---------+------+
| empno | ename | job     | sal     | mgr  |
+-------+-------+---------+---------+------+
|  7566 | JONES | MANAGER | 2975.00 | 7839 |
|  7698 | BLAKE | MANAGER | 2850.00 | 7839 |
|  7782 | CLARK | MANAGER | 2450.00 | 7839 |
+-------+-------+---------+---------+------+
3 rows in set (0.00 sec)
```

(p.56) OR

```
mysql> SELECT empno,ename,job,sal,mgr
    -> FROM   emp
    -> WHERE  sal>2000 OR job = 'manager';
+-------+-------+-----------+---------+------+
| empno | ename | job       | sal     | mgr  |
+-------+-------+-----------+---------+------+
|  7566 | JONES | MANAGER   | 2975.00 | 7839 |
|  7698 | BLAKE | MANAGER   | 2850.00 | 7839 |
|  7782 | CLARK | MANAGER   | 2450.00 | 7839 |
|  7788 | SCOTT | ANALYST   | 3000.00 | 7566 |
|  7839 | KING  | PRESIDENT | 5000.00 | NULL |
|  7902 | mary  | ANALYST   | 3000.00 | 7566 |
+-------+-------+-----------+---------+------+
6 rows in set (0.00 sec)
```

(p.57) NOT

```
mysql> SELECT empno,ename,job,sal,mgr
    -> FROM   emp
    -> WHERE  NOT(sal>2000 OR job = 'manager');
+-------+--------+----------+---------+------+
| empno | ename  | job      | sal     | mgr  |
+-------+--------+----------+---------+------+
|  7369 | SMITH  | CLERK    |  800.00 | 7902 |
|  7499 | ALLEN  | SALESMAN | 2000.00 | 7698 |
|  7654 | MARTIN | SALESMAN | 1250.00 | 7698 |
|  7844 | TURNER | SALESMAN | 1500.00 | 7698 |
|  7876 | ADAMS  | CLERK    | 1100.00 | 7788 |
|  7934 | MILLER | CLERK    | 1300.00 | 7782 |
+-------+--------+----------+---------+------+
6 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="特殊運算子BETWEEN AND,IN,IS NULL" %}
(p.58) **BETWEEN AND**查詢薪水介於2000到3500之間的員工

```
mysql> SELECT empno,ename,job,sal
    -> FROM   emp
    -> WHERE  sal BETWEEN 2000 AND 3500;
+-------+-------+----------+---------+
| empno | ename | job      | sal     |
+-------+-------+----------+---------+
|  7499 | ALLEN | SALESMAN | 2000.00 |
|  7566 | JONES | MANAGER  | 2975.00 |
|  7698 | BLAKE | MANAGER  | 2850.00 |
|  7782 | CLARK | MANAGER  | 2450.00 |
|  7788 | SCOTT | ANALYST  | 3000.00 |
|  7902 | mary  | ANALYST  | 3000.00 |
+-------+-------+----------+---------+
6 rows in set (0.00 sec)
```

(p.59) **IN** 列出職務為salesman或manager的員工

```
mysql> SELECT empno,ename,job,sal
    -> FROM   emp
    -> WHERE  job IN ('salesman','manager');
+-------+--------+----------+---------+
| empno | ename  | job      | sal     |
+-------+--------+----------+---------+
|  7499 | ALLEN  | SALESMAN | 2000.00 |
|  7566 | JONES  | MANAGER  | 2975.00 |
|  7654 | MARTIN | SALESMAN | 1250.00 |
|  7698 | BLAKE  | MANAGER  | 2850.00 |
|  7782 | CLARK  | MANAGER  | 2450.00 |
|  7844 | TURNER | SALESMAN | 1500.00 |
+-------+--------+----------+---------+
6 rows in set (0.01 sec)
```

(p.63) **IS NULL** 找出公司老闆的資料(mgr是null的員工)

```
mysql> SELECT empno,ename,job,sal,mgr
    -> FROM emp
    -> WHERE mgr IS NULL;
+-------+-------+-----------+---------+------+
| empno | ename | job       | sal     | mgr  |
+-------+-------+-----------+---------+------+
|  7839 | KING  | PRESIDENT | 5000.00 | NULL |
+-------+-------+-----------+---------+------+
1 row in set (0.00 sec)
```
{% endtab %}

{% tab title="特殊運算子LIKE" %}
(p.60) **LIKE** 列出姓名以A開頭的員工

```
mysql> SELECT empno,ename,job,sal
    -> FROM   emp
    -> WHERE  ename LIKE 'A%';
+-------+-------+----------+---------+
| empno | ename | job      | sal     |
+-------+-------+----------+---------+
|  7499 | ALLEN | SALESMAN | 2000.00 |
|  7876 | ADAMS | CLERK    | 1100.00 |
+-------+-------+----------+---------+
2 rows in set (0.00 sec)
```

```
-- (p.61)列出姓名以N結尾的員工
mysql> SELECT empno,ename,job,sal
    -> FROM   emp
    -> WHERE  ename LIKE '%N';
+-------+--------+----------+---------+
| empno | ename  | job      | sal     |
+-------+--------+----------+---------+
|  7499 | ALLEN  | SALESMAN | 2000.00 |
|  7654 | MARTIN | SALESMAN | 1250.00 |
+-------+--------+----------+---------+
2 rows in set (0.00 sec)
```

```
-- (p.61) 列出姓名中含有T的員工
mysql> SELECT empno,ename,job,sal
    -> FROM   emp
    -> WHERE  ename LIKE '%T%';
+-------+--------+----------+---------+
| empno | ename  | job      | sal     |
+-------+--------+----------+---------+
|  7369 | SMITH  | CLERK    |  800.00 |
|  7654 | MARTIN | SALESMAN | 1250.00 |
|  7788 | SCOTT  | ANALYST  | 3000.00 |
|  7844 | TURNER | SALESMAN | 1500.00 |
+-------+--------+----------+---------+
4 rows in set (0.00 sec)
```

```
-- (p.62) 列出姓名第二個字為A的員工
mysql> SELECT empno,ename,job,sal
    -> FROM   emp
    -> WHERE  ename LIKE '_A%';
+-------+--------+----------+---------+
| empno | ename  | job      | sal     |
+-------+--------+----------+---------+
|  7521 | WARD   | SALESMAN | 1250.00 |
|  7654 | MARTIN | SALESMAN | 1250.00 |
|  7900 | JAMES  | CLERK    |  950.00 |
+-------+--------+----------+---------+
3 rows in set (0.01 sec)
```
{% endtab %}

{% tab title="NOT" %}
* NOT BETWEEN..AND..
* NOT IN
* NOT LIKE
* **IS NOT NULL**

(p.64) **NOT** 列出除了manager & salesman以外的員工

```
mysql> SELECT empno,ename,job,sal,deptno
    -> FROM   emp
    -> WHERE  job NOT IN ('salesman','manager');
+-------+--------+-----------+---------+--------+
| empno | ename  | job       | sal     | deptno |
+-------+--------+-----------+---------+--------+
|  7369 | SMITH  | CLERK     |  800.00 |     20 |
|  7788 | SCOTT  | ANALYST   | 3000.00 |     20 |
|  7839 | KING   | PRESIDENT | 5000.00 |     10 |
|  7876 | ADAMS  | CLERK     | 1100.00 |     20 |
|  7900 | JAMES  | CLERK     |  950.00 |     30 |
|  7902 | FORD   | ANALYST   | 3000.00 |     20 |
|  7934 | MILLER | CLERK     | 1300.00 |     10 |
+-------+--------+-----------+---------+--------+
7 rows in set (0.00 sec)
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="列舉式CASE(p.66)" %}
SELECT ...\
FROM ...\
&#x20;　　　CASE 欄位名\
　　　　　　WHEN '條件1' THEN 執行1\
　　　　　　WHEN '條件2' THEN 執行2\
　　　　　　WHEN '條件3' THEN 執行3\
　　　　　　ELSE 執行4\
　　　　　END 執行後新欄位名稱;-- (以下代入例子)

```
SELECT empno, ename, sal, job,
    CASE job
      WHEN 'President' THEN Sal*1.5
      WHEN 'Manager' THEN Sal*1.3
      WHEN 'Analyst' THEN Sal*1.2
      ELSE Sal*1
    END sal
FROM emp;
+-------+--------+---------+-----------+----------+
| empno | ename  | sal     | job       | sal      |
+-------+--------+---------+-----------+----------+
|  7369 | SMITH  |  800.00 | CLERK     |   800.00 |
|  7499 | ALLEN  | 1600.00 | SALESMAN  |  1600.00 |
|  7521 | WARD   | 1250.00 | SALESMAN  |  1250.00 |
|  7566 | JONES  | 2975.00 | MANAGER   | 3867.500 |
|  7654 | MARTIN | 1250.00 | SALESMAN  |  1250.00 |
|  7698 | BLAKE  | 2850.00 | MANAGER   | 3705.000 |
|  7782 | CLARK  | 2450.00 | MANAGER   | 3185.000 |
|  7788 | SCOTT  | 3000.00 | ANALYST   | 3600.000 |
|  7839 | KING   | 5000.00 | PRESIDENT | 7500.000 |
|  7844 | TURNER | 1500.00 | SALESMAN  |  1500.00 |
|  7876 | ADAMS  | 1100.00 | CLERK     |  1100.00 |
|  7900 | JAMES  |  950.00 | CLERK     |   950.00 |
|  7902 | FORD   | 3000.00 | ANALYST   | 3600.000 |
|  7934 | MILLER | 1300.00 | CLERK     |  1300.00 |
+-------+--------+---------+-----------+----------+
14 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="條件式CASE(p.67)" %}
SELECT ...\
FROM ...\
WHERE\
　　CASE 欄位名 BETWEEN x1 AND y1 THEN 執行1\
　　　　　欄位名 BETWEEN x2 AND y2 THEN 執行2\
　　　　　欄位名 BETWEEN x3 AND y3 THEN 執行3\
　　　　　ELSE 執行4\
　　　　END 執行後新欄位名稱;-- (以下帶入例子)

```
SELECT empno, ename,sal,
　　CASE 
      WHEN  sal BETWEEN 0    AND 1000 THEN 'A'
      WHEN  sal BETWEEN 1001 AND 2000 THEN 'B'
      WHEN  sal BETWEEN 2001 AND 3000 THEN 'C'
      WHEN  sal BETWEEN 3001 AND 4000 THEN 'D'
      ELSE 'E'
　　END sal
FROM emp;
```
{% endtab %}
{% endtabs %}

## 條件篩選ORDER BY

SELECT ...\
FROM ...\
WHERE  …\
ORDER BY 欄位名稱 | 欄位數 | 欄位別名 \[ASC升冪預設 | DESC降冪];

以下範例

{% tabs %}
{% tab title="基本" %}
(p.68) 沒有指定的欄位也可以做排序

```
mysql> SELECT   empno,ename,sal--  ←－－－－－－－－－－－－－－－－－－-
    -> FROM     emp            --                                  |
    -> WHERE    deptno =10     --                                  |
    -> ORDER BY hiredate; -- 🔹「hiredate」沒在指定欄位,也可以用以做排序
+-------+--------+---------+
| empno | ename  | sal     |
+-------+--------+---------+
|  7782 | CLARK  | 2450.00 |
|  7839 | KING   | 5000.00 |
|  7934 | MILLER | 1300.00 |
+-------+--------+---------+
3 rows in set (0.00 sec)
```

```
-- (p.70)依欄位別名排序
mysql> SELECT   empno,ename,sal*12 annsal-- 🔹annsal是別名
    -> FROM     emp
    -> WHERE    deptno = 10
    -> ORDER BY annsal;                  -- 🔹用別名annsal排序
+-------+--------+----------+
| empno | ename  | annsal   |
+-------+--------+----------+
|  7934 | MILLER | 15600.00 |
|  7782 | CLARK  | 29400.00 |
|  7839 | KING   | 60000.00 |
+-------+--------+----------+
3 rows in set (0.00 sec)
```

```
-- (p.70)依運算式排序
mysql> SELECT   empno,ename,sal+comm bonus
    -> FROM     emp
    -> WHERE    deptno = 30
    -> ORDER BY sal+comm;-- 🔹
+-------+--------+---------+
| empno | ename  | bonus   |
+-------+--------+---------+
|  7698 | BLAKE  |    NULL |
|  7900 | JAMES  |    NULL |
|  7844 | TURNER | 1500.00 |
|  7521 | WARD   | 1750.00 |
|  7499 | ALLEN  | 1900.00 |
|  7654 | MARTIN | 2650.00 |
+-------+--------+---------+
6 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="降冪" %}
範例一：對薪資做降冪排序 (p.69)\
`SELECT empno, ename, sal`\
`FROM emp`\
`WHERE deptno = 10`\
`ORDER BY sal DESC;🔶`

```
+-------+--------+---------+
| empno | ename  | sal     |
+-------+--------+---------+
|  7839 | KING   | 5000.00 |
|  7782 | CLARK  | 2450.00 |
|  7934 | MILLER | 1300.00 |
+-------+--------+---------+
3 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="第x欄" %}
範例二：對第三直排做排序(p.71)\
`SELECT *`\
&#x20;`FROM emp` \
`WHERE deptno = 20` \
`ORDER BY 3;🔶`

```
+-------+-------+---------+------+---------------------+---------+------+--------+
| EMPNO | ENAME | JOB     | MGR  | HIREDATE            | SAL     | COMM | DEPTNO |
+-------+-------+---------+------+---------------------+---------+------+--------+
|  7788 | SCOTT | ANALYST | 7566 | 1982-12-09 00:00:00 | 3000.00 | NULL |     20 |
|  7902 | FORD  | ANALYST | 7566 | 1981-12-03 00:00:00 | 3000.00 | NULL |     20 |
|  7369 | SMITH | CLERK   | 7902 | 1980-12-17 00:00:00 |  800.00 | NULL |     20 |
|  7876 | ADAMS | CLERK   | 7788 | 1983-01-12 00:00:00 | 1100.00 | NULL |     20 |
|  7566 | JONES | MANAGER | 7839 | 1981-04-02 00:00:00 | 2975.00 | NULL |     20 |
+-------+-------+---------+------+---------------------+---------+------+--------+
5 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="多欄" %}
範例三：多欄排序，以「逗號」分隔(p.72)

* 對 \[部門] 做升冪排序
* 對 \[職稱] 做升冪排序
* 對 \[第六直欄] 做降冪排序
* 對 \[第一欄]做升冪排序

`SELECT *`\
`FROM emp`\
`ORDER BY deptno, job, 6 DESC, 1;🔶`

```
+-------+--------+-----------+------+---------------------+---------+---------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE            | SAL     | COMM    | DEPTNO |
+-------+--------+-----------+------+---------------------+---------+---------+--------+
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 00:00:00 | 1300.00 |    NULL |     10 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 00:00:00 | 2450.00 |    NULL |     10 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 00:00:00 | 5000.00 |    NULL |     10 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1982-12-09 00:00:00 | 3000.00 |    NULL |     20 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 00:00:00 | 3000.00 |    NULL |     20 |
|  7876 | ADAMS  | CLERK     | 7788 | 1983-01-12 00:00:00 | 1100.00 |    NULL |     20 |
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 00:00:00 |  800.00 |    NULL |     20 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 00:00:00 | 2975.00 |    NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 00:00:00 |  950.00 |    NULL |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 00:00:00 | 2850.00 |    NULL |     30 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 00:00:00 | 1600.00 |  300.00 |     30 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 00:00:00 | 1500.00 |    0.00 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 00:00:00 | 1250.00 |  500.00 |     30 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 00:00:00 | 1250.00 | 1400.00 |     30 |
+-------+--------+-----------+------+---------------------+---------+---------+--------+
14 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="LIMIT" %}
範例四：只顯示指定筆數(p.73)\
(例如有14橫列，LIMIT 5 就是指  只顯示前面五筆。)

`SELECT ename, sal, job`\
`FROM emp`\
`ORDER BY sal DESC🔷`\
`LIMIT 5;🔶`

```
+-------+---------+-----------+
| ename | sal     | job       |
+-------+---------+-----------+
| KING  | 5000.00 | PRESIDENT |
| FORD  | 3000.00 | ANALYST   |
| SCOTT | 3000.00 | ANALYST   |
| JONES | 2975.00 | MANAGER   |
| BLAKE | 2850.00 | MANAGER   |
+-------+---------+-----------+
5 rows in set (0.00 sec)
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
不在「SELECT」的欄位也可以做排序。
{% endhint %}

## 作業練習－DQL-SELECT(p.49)

1. 建立一個查詢來顯示部門(dept)資料表中的所有資料。
2. 建立一個查詢來顯示每一位員工的姓名(name)、職稱(job)、到職日(hire date)、員工編號(employee number)，並將員工編號顯示在最前面。
3. 建立一個查詢來顯示所有員工所擔任的職稱有哪些(重複資料只顯示一次)。
4. 建立一個查詢來顯示每一位員工的姓名、職稱、到職日、員編，並將員編顯示在最前面。\
   將資料表頭重新命名:emp#,Employee,job,hire date。
5. 建立一個查詢將姓名、職稱串接為一個資料項(資料中間利用一個空白和一個逗號做區隔)，將表頭重新命名為employee and title。

{% tabs %}
{% tab title="1" %}
```sql
-- 建立一個查詢來顯示部門(dept)資料表中的所有資料。
SELECT * 
	FROM dept;
/*
+--------+------------+----------+
| DEPTNO | DNAME      | LOC      |
+--------+------------+----------+
|     10 | ACCOUNTING | NEW YORK |
|     20 | RESEARCH   | DALLAS   |
|     30 | SALES      | CHICAGO  |
|     40 | OPERATIONS | BOSTON   |
+--------+------------+----------+
4 rows in set (0.00 sec)	*/
```
{% endtab %}

{% tab title="2" %}
```sql
/*建立一個查詢來顯示每一位員工的
姓名(name)、職稱(job)、到職日(hire date)、員工編號(employee number)，
並將員工編號顯示在最前面。
*/
SELECT empno, ename, job, hiredate 
	FROM emp;  
/*
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
14 rows in set (0.00 sec)*/
```
{% endtab %}

{% tab title="3" %}
```sql
-- 建立一個查詢來顯示所有員工所擔任的職稱有哪些(重複資料只顯示一次)。
SELECT DISTINCT job 
	FROM emp;
/*
+-----------+
| job       |
+-----------+
| CLERK     |
| SALESMAN  |
| MANAGER   |
| ANALYST   |
| PRESIDENT |
+-----------+
5 rows in set (0.00 sec)*/
```
{% endtab %}

{% tab title="4" %}
```sql
/*建立一個查詢來顯示每一位員工的姓名、職稱、到職日、員編，並將員編顯示在最前面。
將資料表頭重新命名:emp#,Employee,job,hire date。
*/
SELECT empno 'Emp#', ename 'Employee', job 'Job', hiredate 'Hire Date' 
	FROM emp;
/*
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
14 rows in set (0.00 sec)*/
```
{% endtab %}

{% tab title="5" %}
```sql
/*建立一個查詢將姓名、職稱串接為一個資料項(資料中間利用一個空白和一個逗號做區隔)，
將表頭重新命名為employee and title。
*/
SELECT CONCAT(ename,', ',job) 'Employee and Title' 
	FROM emp;
/*
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
14 rows in set (0.00 sec)*/
```
{% endtab %}
{% endtabs %}



## 作業練習－DQL-WHERE(p.73)

1. 顯示出所有員工薪資超過2850元的員工姓名和薪資。
2. 顯示員編7566員工姓名及其所屬部門。
3. 顯示薪資不介於1500\~2850元的員工姓名及薪資。
4. 顯示於1981-2-20和1981-5-1間進入公司的員工姓名、職稱、到職日，並依到職日由小到大排序。
5. 顯示部門10和30所有員工姓名及其所屬部門編號，依名字英文字母排序。
6. 顯示薪資超過1500且在10或30部門工作員工之姓名和薪資，\
   表頭命名為employee和monthly salary。
7. 顯示於1982年進公司的所有員工姓名、職稱、到職日。
8. 顯示沒有主管的員工姓名和職稱。
9. 顯示所有有賺取佣金的員工姓名、薪資、佣金，並依薪資和佣金做降冪排序。
10. 顯示所有名字裡第三個英文字母為A的員工之姓名與職稱
11. 顯示名字裡有兩個L且在30部門工作或經理是7782的員工姓名、經理員編及其所屬部門編號。
12. 顯示值稱為Clerk或analyst且薪水不等於1000,3000,5000的員工姓名、職稱、薪資。
13. 顯示佣金比薪水的1.1倍還多的員工姓名、薪資、佣金。

{% tabs %}
{% tab title="1" %}
```
-- 顯示出所有員工薪資超過2850元的員工姓名和薪資。
SELECT  ename, sal 
	FROM  emp 
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
SELECT  ename, deptno 
	FROM  emp 
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

SELECT  ename, sal 
	FROM  emp 
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
SELECT     ename, job, hiredate 
	FROM     emp 
  WHERE    hiredate BETWEEN '1981-2-20' AND '1981-5-1' 
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
SELECT     ename, deptno 
	FROM     emp 
  WHERE    deptno IN (10,20) 
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
SELECT  ename 'Employee' ,sal 'Monthly Salary' 
	FROM  emp 
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
SELECT  ename, job, hiredate
	FROM  emp 
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
SELECT    ename, job 
	FROM    emp 
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
SELECT     ename, sal, comm 
	FROM     emp 
  WHERE    comm IS NOT NULL AND comm<>0 
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
SELECT  ename, job 
	FROM  emp 
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
-- 顯示名字裡有兩個L且在30部門工作或經理是7782的員工姓名、經理員編及其所屬部門編號。
SELECT    ename, mgr, deptno 
	FROM    emp 
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
SELECT  ename, job, sal 
	FROM  emp 
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
SELECT  ename, sal, comm 
	FROM  emp 
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
