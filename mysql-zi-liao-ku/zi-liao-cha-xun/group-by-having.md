---
description: 參照講義p.99~p.118
---

# GROUP BY、HAVING

## 群組彙總函數(p.100)

| 函數                       | 功能           |
| ------------------------ | ------------ |
| COUNT(\*)                | 資料的筆數        |
| COUNT(_column_)          | 欄位不為空值的筆數    |
| COUNT(DISTINCT _column_) | 去除重複列不為空值的筆數 |
| MAX(_column_)            | 欄位中最大的值      |
| MIN(_column_)            | 欄位中最小的值      |
| SUM(_column_)            | ​欄位的加總       |
| AVG(_column_)            | 欄位的平均值       |

下面範例

{% tabs %}
{% tab title="COUNT1" %}
`-- COUNT對照`\
`SELECT *`\
`FROM emp`\
`WHERE deptno = 10;`\
&#x9;`-- 🔶COUNT(*)`\
&#x9;`SELECT COUNT(*)`\
&#x9;`FROM emp`\
&#x9;`WHERE deptno = 10;`

```
-- (p.101)
+----------+
| COUNT(*) |
+----------+
|        3 |
+----------+
1 row in set (0.00 sec)
```

```
-- 對照表
mysql> SELECT *
    -> FROM   emp
    -> WHERE  deptno=10;
+-------+--------+-----------+------+---------------------+---------+------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE            | SAL     | COMM | DEPTNO |
+-------+--------+-----------+------+---------------------+---------+------+--------+
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 00:00:00 | 2450.00 | NULL |     10 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 00:00:00 | 5000.00 | NULL |     10 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 00:00:00 | 1300.00 | NULL |     10 |
+-------+--------+-----------+------+---------------------+---------+------+--------+
3 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="COUNT2" %}
(p.101) 傳回資料表中的資料列數

```
mysql> SELECT comm
    -> FROM emp
    -> WHERE deptno = 30;
+---------+
| comm    |
+---------+
|  300.00 |
|  500.00 |
| 1400.00 |
|    NULL |
|    0.00 |
|    NULL |
+---------+

-- 🔶COUNT(column | expr)
mysql> SELECT COUNT(comm)
    -> FROM emp
    -> WHERE deptno = 30;
+-------------+
| COUNT(comm) |
+-------------+
|           4 |
+-------------+
1 row in set (0.00 sec)
```
{% endtab %}

{% tab title="DISTINCT" %}
`SELECT DISTINCT comm`\
`FROM emp`\
`WHERE deptno = 30;`\
&#x9;`-- 🔶COUNT(DISTINCT column | expr)`\
&#x9;`SELECT DISTINCT COUNT(comm)`\
&#x9;`FROM emp`\
&#x9;`WHERE deptno = 30;`

```
-- (p.102) 傳回欄位或運算式中去除重複資料的資料列數，但不包含空值。(p.102)
mysql> SELECT DISTINCT comm
    -> FROM emp
    -> WHERE deptno = 30;
+---------+
| comm    |
+---------+
|  300.00 |
|  500.00 |
| 1400.00 |
|    NULL |
|    0.00 |
+---------+
5 rows in set (0.00 sec)


-- 🔶COUNT(DISTINCT column | expr)
mysql> SELECT DISTINCT COUNT(comm)
    -> FROM emp
    -> WHERE deptno = 30;
+-------------+
| COUNT(comm) |
+-------------+
|           4 |
+-------------+
1 row in set (0.00 sec)
```
{% endtab %}

{% tab title="MAX" %}
```
-- MAX(column) | expr)對照(p.102)
mysql> SELECT sal
    -> FROM emp
    -> WHERE deptno = 30;
+---------+
| sal     |
+---------+
| 1600.00 |
| 1250.00 |
| 1250.00 |
| 2850.00 |
| 1500.00 |
|  950.00 |
+---------+
6 rows in set (0.00 sec)


	-- 🔶MAX(column) | expr)最大值
	mysql>     SELECT MAX(sal)
    ->     FROM emp
    ->     WHERE deptno = 30;
+----------+
| MAX(sal) |
+----------+
|  2850.00 |
+----------+
1 row in set (0.00 sec)

```
{% endtab %}

{% tab title="MIN" %}
```
-- MIN(column) | expr)對照(p.103)
mysql> SELECT sal
    -> FROM emp
    -> WHERE deptno = 30;
+---------+
| sal     |
+---------+
| 1600.00 |
| 1250.00 |
| 1250.00 |
| 2850.00 |
| 1500.00 |
|  950.00 |
+---------+
6 rows in set (0.00 sec)


-- 🔶MIN(column) | expr)最小值
mysql> SELECT MIN(sal)
    ->     FROM emp
    ->     WHERE deptno = 30;
+----------+
| MIN(sal) |
+----------+
|   950.00 |
+----------+
1 row in set (0.00 sec)
```
{% endtab %}

{% tab title="SUM" %}
```
-- SUM(column) | expr)對照(p.103)
mysql> SELECT sal
    -> FROM emp
    -> WHERE deptno = 30;
+---------+
| sal     |
+---------+
| 1600.00 |
| 1250.00 |
| 1250.00 |
| 2850.00 |
| 1500.00 |
|  950.00 |
+---------+
6 rows in set (0.00 sec)


-- 🔶SUM(column) | expr)加總
mysql> SELECT SUM(sal)
    ->     FROM emp
    ->     WHERE deptno = 30;
+----------+
| SUM(sal) |
+----------+
|  9400.00 |
+----------+
1 row in set (0.00 sec)
```
{% endtab %}

{% tab title="AVG" %}
```
-- AVG(column) | expr)對照(p.104)
+---------+
| comm    |
+---------+
|  300.00 |
|  500.00 |
| 1400.00 |
|    NULL |
|    0.00 |
|    NULL |
+---------+


-- 🔶AVG(column) | expr) / COUNT(column)平均值(不含null人頭)
-- (1400+3000+0+500)÷4

mysql> SELECT AVG(comm)
    -> FROM emp
    -> WHERE deptno = 30;
+------------+
| AVG(comm)  |
+------------+
| 550.000000 |
+------------+


-- 🔶AVG(IFNULL(column) | expr,0))平均值(含null人頭)
-- (1400+3000+0+500)÷6
-- 另一個算法：SUM(column) / COUNT(*)

mysql> SELECT AVG(IFNULL(comm,0)) AVG
    -> FROM emp
    -> WHERE deptno = 30;
+------------+
| AVG        |
+------------+
| 366.666667 |
+------------+
```
{% endtab %}

{% tab title="綜合" %}
\-- 群組函數(p.105)

```
mysql> SELECT SUM(sal),MIN(sal),MAX(sal),AVG(sal),COUNT(*)
    -> FROM emp
    -> WHERE deptno = 30;
+----------+----------+----------+-------------+----------+
| SUM(sal) | MIN(sal) | MAX(sal) | AVG(sal)    | COUNT(*) |
+----------+----------+----------+-------------+----------+
|  9400.00 |   950.00 |  2850.00 | 1566.666667 |        6 |
+----------+----------+----------+-------------+----------+
1 row in set (0.00 sec)
```
{% endtab %}
{% endtabs %}

## 資料分組GROUP BY(p.106)

**`GROUP BY`** _欄位名_

下面範例

{% tabs %}
{% tab title="分組" %}
```
-- GROUP BY資料分組(p.107)
mysql> SELECT    deptno, SUM(sal)
    -> FROM      emp
    -> GROUP BY  deptno;
+--------+----------+
| deptno | SUM(sal) |
+--------+----------+
|     10 |  8750.00 |
|     20 | 10875.00 |
|     30 |  9400.00 |
+--------+----------+
```

```
-- NULL自己一組(p.108)
mysql> SELECT   comm, COUNT(*)
    -> FROM     emp
    -> GROUP BY comm;
+---------+----------+
| comm    | COUNT(*) |
+---------+----------+
|    NULL |       10 |
|  300.00 |        1 |
|  500.00 |        1 |
| 1400.00 |        1 |
|    0.00 |        1 |
+---------+----------+
```

```
-- 使用ORDER BY (p.108)
mysql> SELECT   deptno,SUM(sal)
    -> FROM     emp
    -> GROUP BY deptno
    -> ORDER BY 2;
+--------+----------+
| deptno | SUM(sal) |
+--------+----------+
|     10 |  8750.00 |
|     30 |  9400.00 |
|     20 | 10875.00 |
+--------+----------+
```
{% endtab %}

{% tab title="多欄分組" %}
\-- 多欄分組(多條件中都相符才歸為一組)(p.109)

```
mysql> SELECT   deptno,job,COUNT(*)
    -> FROM     emp
    -> GROUP BY deptno, job
    -- 🔹deptno和job兩個都符合才算一組
+--------+-----------+----------+
| deptno | job       | COUNT(*) |
+--------+-----------+----------+
|     10 | CLERK     |        1 |
|     10 | MANAGER   |        1 |
|     10 | PRESIDENT |        1 |
 -------- ----------- ---------- 
|     20 | ANALYST   |        2 |
|     20 | CLERK     |        2 |
|     20 | MANAGER   |        1 |
 -------- ----------- ---------- 
|     30 | CLERK     |        1 |
|     30 | MANAGER   |        1 |
|     30 | SALESMAN  |        4 |
+--------+-----------+----------+
```
{% endtab %}
{% endtabs %}

## 篩選分組資料 HAVING(p.110)

下面範例

{% tabs %}
{% tab title="分組篩選" %}
```
-- (p.109)
mysql> SELECT deptno, MAX(sal) SalMax
    -> FROM emp
    -> GROUP BY deptno
    -> HAVING MAX(sal) > 2900;
+--------+---------+
| deptno | SalMax  |
+--------+---------+
|     10 | 5000.00 |
|     20 | 3000.00 |
+--------+---------+

mysql> SELECT   deptno, sal
    -> FROM     emp;
+--------+---------+
| deptno | sal     |
+--------+---------+
|     10 | 5000.00 |🔹
|     10 | 2450.00 |
|     10 | 1300.00 |

|     20 | 3000.00 |🔹
|     20 | 3000.00 |🔹
|     20 | 2975.00 |
|     20 | 1100.00 |
|     20 |  800.00 |

|     30 | 2850.00 |🔹
|     30 | 1600.00 |
|     30 | 1500.00 |
|     30 | 1250.00 |
|     30 | 1250.00 |
|     30 |  950.00 |
+--------+---------+
```
{% endtab %}

{% tab title="分組資料串接" %}
\-- GROUP\_CONCAT分組資料串接\
\-- SEPARATOR ==>用甚麼隔開\
\-- 範例：該部門有哪些職位、同部門去除重複的職位(p.117)

```
mysql> SELECT deptno, GROUP_CONCAT(DISTINCT job SEPARATOR ',') jobs
    -> FROM emp
    -> GROUP BY deptno;
+--------+-------------------------+
| deptno | jobs                    |
+--------+-------------------------+
|     10 | CLERK,MANAGER,PRESIDENT |
|     20 | ANALYST,CLERK,MANAGER   |
|     30 | CLERK,MANAGER,SALESMAN  |
+--------+-------------------------+
```
{% endtab %}
{% endtabs %}



## 作業練習－DQL-Group by(p.117)

1. 顯示所有員工的最高、最低、總和、平均薪資，表頭命名maximum,minimum,sum,average，顯示結果四捨五入取整數。
2. 顯示每種職稱的最低、最高、總和、平均薪資。
3. 顯示每種職稱人數。
4. 顯示資料項number of managers 來表示擔任主管的人數。
5. 顯示資料項difference來表示公司中最高和最低薪水間的差額。
6. 🟡顯示每位主管的員工編號及該主管下屬員工最低薪資，排除沒有主管和下屬員工最低薪資少於1000的主管，並以下屬員工最低薪資做降冪排序。
7. 顯示在1980,1981,1982,1983年到職的員工數量，並給該資料項一個合適的名稱。

{% tabs %}
{% tab title="1" %}
```
/*顯示所有員工的最高、最低、總和、平均薪資，
表頭命名maximum,minimum,sum,average，顯示結果四捨五入取整數。*/
SELECT ROUND(MAX(sal),0) 'Maximum',  
		   ROUND(MIN(sal),0) 'Minimum', 
       ROUND(SUM(sal),0) 'SUM', 
       ROUND(AVG(sal),0) 'Average' 
FROM emp;
+---------+---------+-------+---------+
| Maximum | Minimum | SUM   | Average |
+---------+---------+-------+---------+
|    5000 |     800 | 29025 |    2073 |
+---------+---------+-------+---------+
1 row in set (0.03 sec)
```
{% endtab %}

{% tab title="2" %}
```
-- 顯示每種職稱的最低、最高、總和、平均薪資。
SELECT job, MAX(sal), MIN(sal), SUM(sal), AVG(sal) 
FROM emp 
GROUP BY JOB;
+-----------+----------+----------+----------+-------------+
| job       | MAX(sal) | MIN(sal) | SUM(sal) | AVG(sal)    |
+-----------+----------+----------+----------+-------------+
| CLERK     |  1300.00 |   800.00 |  4150.00 | 1037.500000 |
| SALESMAN  |  1600.00 |  1250.00 |  5600.00 | 1400.000000 |
| MANAGER   |  2975.00 |  2450.00 |  8275.00 | 2758.333333 |
| ANALYST   |  3000.00 |  3000.00 |  6000.00 | 3000.000000 |
| PRESIDENT |  5000.00 |  5000.00 |  5000.00 | 5000.000000 |
+-----------+----------+----------+----------+-------------+
5 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="3" %}
```
-- 顯示每種職稱人數。
SELECT job, COUNT(*) 
FROM emp 
GROUP BY JOB;
+-----------+----------+
| job       | COUNT(*) |
+-----------+----------+
| CLERK     |        4 |
| SALESMAN  |        4 |
| MANAGER   |        3 |
| ANALYST   |        2 |
| PRESIDENT |        1 |
+-----------+----------+
5 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="4" %}
```
-- 顯示資料項number of managers 來表示擔任主管的人數。
SELECT count(*) 'Number of Managers' 
FROM emp 
WHERE job='MANAGER';
+--------------------+
| Number of Managers |
+--------------------+
|                  3 |
+--------------------+
1 row in set (0.00 sec)
```
{% endtab %}

{% tab title="5" %}
```
-- 顯示資料項difference來表示公司中最高和最低薪水間的差額。
SELECT MAX(sal)-MIN(sal) 'DIFFERENCE' 
FROM emp;
+------------+
| DIFFERENCE |
+------------+
|    4200.00 |
+------------+
1 row in set (0.04 sec)
```
{% endtab %}

{% tab title="6🟡" %}
```
/*顯示每位主管的員工編號及該主管下屬員工最低薪資，
排除沒有主管和下屬員工最低薪資少於1000的主管，並以下屬員工最低薪資做降冪排序。*/
SELECT mgr, MIN(sal) 
FROM emp 
GROUP BY mgr 
HAVING mgr IS NOT NULL AND MIN(sal)>1000 
ORDER BY MIN(sal) DESC; 
+------+----------+
| mgr  | MIN(sal) |
+------+----------+
| 7566 |  3000.00 |
| 7839 |  2450.00 |
| 7782 |  1300.00 |
| 7788 |  1100.00 |
+------+----------+
4 rows in set (0.02 sec)
```
{% endtab %}

{% tab title="7" %}
```
-- 顯示在1980,1981,1982,1983年到職的員工數量，並給該資料項一個合適的名稱。
SELECT YEAR(hiredate) 'HYear', count(*) 'Number of People' 
FROM emp 
GROUP by YEAR(hiredate) 
HAVING HYear IN (1980,1981,1982,1983); 
+-------+------------------+
| HYear | Number of People |
+-------+------------------+
|  1980 |                1 |
|  1981 |               10 |
|  1982 |                2 |
|  1983 |                1 |
+-------+------------------+
4 rows in set (0.04 sec)
```
{% endtab %}
{% endtabs %}

