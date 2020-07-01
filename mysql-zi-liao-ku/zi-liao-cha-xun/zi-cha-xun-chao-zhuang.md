---
description: 參照講義p.135~p.148
---

# 子查詢\(巢狀\)

## 認識子查詢

執行順序：先執行子查詢\(sub-Query\)再執行主查詢\(Main-query\)。

![](../../.gitbook/assets/image%20%2818%29.png)

### 子查詢的種類

1. 自主子查詢（參照講義p.138）
2. 相關子查詢（參照講義p.144）

### 子查詢的型式

1. 純量（單欄單筆）\(使用頻率80%\)
2. 多值（單欄多筆）\(使用頻率20%\)
3. 多欄位（多欄單筆）
4. 表格值（多欄多筆）

### 子查詢出現的位置

* WHERE 子句
* FROM子句
* HAVING子句

## 子查詢－自主子查詢

{% tabs %}
{% tab title="單筆" %}
```aspnet
/*8-8頁WHERE 子句
 *和JAEMS同部門的員工*/
SELECT empno,ename,deptno
    -> FROM emp
    -> WHERE deptno = (SELECT deptno -- 30
    ->                  FROM emp
    ->                  WHERE ename = 'james');
+-------+--------+--------+
| empno | ename  | deptno |
+-------+--------+--------+
|  7499 | ALLEN  |     30 |
|  7521 | WARD   |     30 |
|  7654 | MARTIN |     30 |
|  7698 | BLAKE  |     30 |
|  7844 | TURNER |     30 |
|  7900 | JAMES  |     30 |
+-------+--------+--------+
6 rows in set (0.00 sec)

-- 8-9列出薪水比員工7566高的所有員工
mysql> use demo;
Database changed
mysql> SELECT empno, ename, sal
    -> FROM emp
    -> WHERE sal > (SELECT sal
    ->             FROM emp
    ->             WHERE empno = 7566);
+-------+-------+---------+
| empno | ename | sal     |
+-------+-------+---------+
|  7788 | SCOTT | 3000.00 |
|  7839 | KING  | 5000.00 |
|  7902 | FORD  | 3000.00 |
+-------+-------+---------+
3 rows in set (0.00 sec)
-- 8-9🔷細項查詢
mysql> SELECT sal
    -> FROM emp
    -> WHERE empno=7566;
+---------+
| sal     |
+---------+
| 2975.00 |
+---------+
1 row in set (0.00 sec)
-- 8-9🔷細項查詢2
mysql> SELECT empno, ename, sal
    -> FROM emp
    -> WHERE sal>2975;
+-------+-------+---------+
| empno | ename | sal     |
+-------+-------+---------+
|  7788 | SCOTT | 3000.00 |
|  7839 | KING  | 5000.00 |
|  7902 | FORD  | 3000.00 |
+-------+-------+---------+
3 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="單筆2" %}
```
-- 8-11 薪水>公司平均薪資的員工
-- 平均薪資AVG(sal)---2073.2143
mysql> SELECT empno, ename, sal
    -> FROM  emp
    -> WHERE sal > (SELECT AVG(sal)
    ->             FROM emp);
+-------+-------+---------+
| empno | ename | sal     |
+-------+-------+---------+
|  7566 | JONES | 2975.00 |
|  7698 | BLAKE | 2850.00 |
|  7782 | CLARK | 2450.00 |
|  7788 | SCOTT | 3000.00 |
|  7839 | KING  | 5000.00 |
|  7902 | FORD  | 3000.00 |
+-------+-------+---------+
6 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="HAVING" %}
```
-- 8-12 應用在HAVING
-- 最低薪資 > 部門20的最低薪資(800) 的部門
mysql> SELECT deptno, MIN(sal)
    -> FROM emp
    -> GROUP BY deptno
    -> HAVING MIN(sal) > (SELECT MIN(sal)
    ->                     FROM emp
    ->                     WHERE deptno = 20);
+--------+----------+
| deptno | MIN(sal) |
+--------+----------+
|     10 |  1300.00 |
|     30 |   950.00 |
+--------+----------+
2 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="多個子查詢" %}
```
-- 8-10 多個子查詢
-- 職稱salesman(7499)、薪水>1300(7934)
mysql> SELECT empno,ename, sal, job
    -> FROM emp
    -> WHERE job = (SELECT job
    ->             FROM emp
    ->             WHERE empno = 7499)
    -> AND sal > (SELECT sal
    ->             FROM emp
    ->             WHERE empno = 7934);
+-------+--------+---------+----------+
| empno | ename  | sal     | job      |
+-------+--------+---------+----------+
|  7499 | ALLEN  | 1600.00 | SALESMAN |
|  7844 | TURNER | 1500.00 | SALESMAN |
+-------+--------+---------+----------+
2 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="IN" %}
```
-- 8-14公司所有主管
/*運算子「=」後只能有一個結果
 *「IN」後的結果可以有多個*/
  mysql> SELECT empno, ename
    -> FROM emp
    -> WHERE empno IN (SELECT mgr
    ->                 FROM emp);
+-------+-------+
| empno | ename |
+-------+-------+
|  7566 | JONES |
|  7698 | BLAKE |
|  7782 | CLARK |
|  7788 | SCOTT |
|  7839 | KING  |
|  7902 | FORD  |
+-------+-------+
6 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="NULL" %}
```
-- 8-15 公司所有職員
-- 結果是NULL ，因為裡面有格子含空值(null比較還是null)
mysql> SELECT empno, ename
    -> FROM emp
    -> WHERE empno NOT IN (SELECT mgr
    ->                     FROM emp);
Empty set (0.00 sec)


-- 8-16=>8-15的解決方案：排除查詢空值資料
SELECT empno, ename
FROM emp
WHERE empno NOT IN (SELECT mgr
			                FROM emp 
            			    WHERE mgr IS NOT NULL);
+-------+--------+
| empno | ename  |
+-------+--------+
|  7369 | SMITH  |
|  7499 | ALLEN  |
|  7521 | WARD   |
|  7654 | MARTIN |
|  7844 | TURNER |
|  7876 | ADAMS  |
|  7900 | JAMES  |
|  7934 | MILLER |
+-------+--------+
8 rows in set (0.00 sec)            
```
{% endtab %}
{% endtabs %}

### 錯誤的範例

{% tabs %}
{% tab title="1" %}
```text
-- 8-13 多筆紀錄的error
-- 其一：子查詢GROUP BY含多筆結果，主查詢WHERE後「=」應只含一筆結果。
mysql> SELECT empno, ename ,sal
    -> FROM emp
    -> WHERE sal = (SELECT MIn(sal)
    ->             FROM emp
    ->             GROUP BY deptno);
ERROR 1242 (21000): Subquery returns more than 1 row
```
{% endtab %}

{% tab title="2" %}
```
-- 8-13 多筆紀錄的error
-- 其二：沒有8000號員工，null比較結果還是null。
mysql> SELECT empno, ename, sal
    -> FROM emp
    -> WHERE sal > (SELECT sal
    ->             FROM emp
    ->             WHERE empno = 8000);
Empty set (0.00 sec)
```
{% endtab %}
{% endtabs %}

### 多筆記錄子查詢

![10~50&#x6578;&#x503C;&#x53EA;&#x662F;&#x8209;&#x4F8B;](../../.gitbook/assets/image%20%287%29.png)

* &lt;ALL：小於子查詢最小值
* &gt;ALL：大於子查詢最大值
* &lt;ANY：小於子查詢最大值
* &gt;ANY：大於子查詢最小值

{% tabs %}
{% tab title="ANY" %}
```text
-- 8-17使用ANY
-- 薪水<  職稱「clerk」(最高薪資1300)  的員工
SELECT empno, ename, job
FROM emp
WHERE sal < ANY (SELECT sal
						　　　FROM emp
						　　　WHERE job = 'CLERK');
+-------+--------+----------+
| empno | ename  | job      |
+-------+--------+----------+
|  7369 | SMITH  | CLERK    |
|  7521 | WARD   | SALESMAN |
|  7654 | MARTIN | SALESMAN |
|  7876 | ADAMS  | CLERK    |
|  7900 | JAMES  | CLERK    |
+-------+--------+----------+
5 rows in set (0.00 sec)


-- 🔷細項查詢
SELECT sal
FROM emp
WHERE job = 'CLERK';
+---------+
| sal     |
+---------+
|  800.00 |
| 1100.00 |
|  950.00 |
| 1300.00 |
+---------+
4 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="ALL" %}
```text
-- 8-18 薪水 > salesman(最高薪資1600)的員工
SELECT empno, ename, job, sal
FROM emp
WHERE sal > ALL (SELECT sal
			FROM emp
			WHERE job = 'salesman');
+-------+-------+-----------+---------+
| empno | ename | job       | sal     |
+-------+-------+-----------+---------+
|  7566 | JONES | MANAGER   | 2975.00 |
|  7698 | BLAKE | MANAGER   | 2850.00 |
|  7782 | CLARK | MANAGER   | 2450.00 |
|  7788 | SCOTT | ANALYST   | 3000.00 |
|  7839 | KING  | PRESIDENT | 5000.00 |
|  7902 | FORD  | ANALYST   | 3000.00 |
+-------+-------+-----------+---------+
6 rows in set (0.00 sec)
			

-- 🔷細項查詢
SELECT sal
FROM emp
WHERE job = 'salesman' ;
+---------+
| sal     |
+---------+
| 1600.00 |
| 1250.00 |
| 1250.00 |
| 1500.00 |
+---------+
4 rows in set (0.00 sec)
```
{% endtab %}
{% endtabs %}

## 子查詢－相關子查詢

依賴外部查詢。子查詢用到主查詢的欄位\(相關\)

{% tabs %}
{% tab title="同表" %}
```text
-- 8-21 每個客戶「最近」跟公司下訂單的日期
-- 沒有「WHERE」結果就會只有一筆
-- 子查詢的WHERE意思是一個客戶一個客戶找
mysql> SELECT ordid, custid, orderdate
    -> FROM ord AS o1
    -> WHERE orderdate = (SELECT MAX(orderdate)
    ->                     FROM ord AS o2
    ->                     WHERE o2.custid = o1.custid)
    -> ORDER BY custid, orderdate;
+-------+--------+---------------------+
| ordid | custid | orderdate           |
+-------+--------+---------------------+
|   613 |    100 | 1987-03-12 00:00:00 |
|   601 |    101 | 1987-01-07 00:00:00 |
|   620 |    102 | 1987-02-15 00:00:00 |
|   616 |    103 | 1987-02-03 00:00:00 |
|   617 |    104 | 1987-02-02 00:00:00 |
|   618 |    105 | 1987-02-05 00:00:00 |
|   607 |    106 | 1986-07-14 00:00:00 |
|   619 |    107 | 1987-02-01 00:00:00 |
|   614 |    108 | 1987-02-01 00:00:00 |
+-------+--------+---------------------+
9 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="同表2" %}
```
-- 8-22 查詢各部門薪資最高的員工資料
mysql> SELECT ename, sal, deptno
    -> FROM emp oe
    -> WHERE sal = (SELECT MAX(sal)
    ->             FROM emp ie
    ->             WHERE ie.deptno = oe.deptno)
    -> ORDER BY deptno;
+-------+---------+--------+
| ename | sal     | deptno |
+-------+---------+--------+
| KING  | 5000.00 |     10 |
| SCOTT | 3000.00 |     20 |
| FORD  | 3000.00 |     20 |
| BLAKE | 2850.00 |     30 |
+-------+---------+--------+
4 rows in set (0.00 sec)
```
{% endtab %}
{% endtabs %}

## EXISTS－存在性測試

* EXISTS 存在性測試，結果只有true \| false
* 語法WHERE \[NOT\] EXISTS \(subquery\)
* 不需要任何欄位或運算式
* 一般子查詢SELECT都用星號「\*」

{% tabs %}
{% tab title="存在" %}
```text
-- 8-25 下過訂單的客戶資料
mysql> SELECT custid, name
    -> FROM customer AS c
    -> WHERE EXISTS (SELECT *
    ->             FROM ord AS o
    ->             WHERE c.custid = o.custid);
+--------+----------------------------------------------+
| custid | name                                         |
+--------+----------------------------------------------+
|    100 | JOCKSPORTS                                   |
|    101 | TKB SPORT SHOP                               |
|    102 | VOLLYRITE                                    |
|    103 | JUST TENNIS                                  |
|    104 | EVERY MOUNTAIN                               |
|    105 | K + T SPORTS                                 |
|    106 | SHAPE UP                                     |
|    107 | WOMENS SPORTS                                |
|    108 | NORTH WOODS HEALTH AND FITNESS SUPPLY CENTER |
+--------+----------------------------------------------+
9 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="不存在" %}
```
-- 8-26 為下過定單的客戶資料(結果是沒有w)
mysql> SELECT custid, name
    -> FROM customer AS c
    -> WHERE NOT EXISTS (SELECT *
    ->                     FROM ord AS o
    ->                     WHERE c.custid = o.custid);
Empty set (0.00 sec)
```
{% endtab %}
{% endtabs %}

## 作業練習

參照講義P.148

9~11較難。

1. 顯示和Blake同部門的所有員工之姓名和進公司日期
2. 顯示所有在Blake之後進公司的員工之姓名及進公司日期。
3. 顯示薪資比公司平均薪資高的所有員工之員工編號，姓名和薪資，並依薪資由高到低排列。
4. 顯示和姓名中包含T的人在相同部門工作的所有員工之員工編號和姓名。
5. 顯示在Dallas工作的所有員工之姓名，部門編號和職稱。
6. 顯示直屬於"KING"的員工之姓名和薪資。
7. 顯示銷售部門"SALES"所有員工之部門編號，姓名和職稱
8. 顯示薪資比公司平均薪資還要高且和姓名中有T的人在相同部門上班的所有員工之員工編號，姓名和薪資。
9. 顯示和賺取佣金的員工之部門編號和薪資都相同的員工之姓名，部門編號和薪資。
10. 顯示和在DALLAS工作的員工之薪資和佣金相同的員工之姓名，部門編號和薪資。
11. 顯示薪資和佣金都和SCOTT相同的所有員工之姓名，進公司日期和薪資。\(不要在結果中顯示SCOTT的資料\)
12. 顯示薪資比所有職稱是"CLERK"還高的員工之姓名，進公司日期和薪資，並將結果依薪資由高志低顯示。

{% tabs %}
{% tab title="1" %}
```text
-- 顯示和Blake同部門的所有員工之姓名和進公司日期
SELECT ename, hiredate 
	FROM emp 
  WHERE deptno = (SELECT deptno 
	                FROM emp 
                  WHERE ename='Blake');
+--------+---------------------+
| ename  | hiredate            |
+--------+---------------------+
| ALLEN  | 1981-02-20 00:00:00 |
| WARD   | 1981-02-22 00:00:00 |
| MARTIN | 1981-09-28 00:00:00 |
| BLAKE  | 1981-05-01 00:00:00 |
| TURNER | 1981-09-08 00:00:00 |
| JAMES  | 1981-12-03 00:00:00 |
+--------+---------------------+
6 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="2" %}
```
-- 顯示所有在Blake之後進公司的員工之姓名及進公司日期。
SELECT ename, hiredate 
	FROM emp 
  WHERE hiredate > (SELECT hiredate 
						        FROM emp 
                    WHERE ename='Blake');
+--------+---------------------+
| ename  | hiredate            |
+--------+---------------------+
| MARTIN | 1981-09-28 00:00:00 |
| CLARK  | 1981-06-09 00:00:00 |
| SCOTT  | 1982-12-09 00:00:00 |
| KING   | 1981-11-17 00:00:00 |
| TURNER | 1981-09-08 00:00:00 |
| ADAMS  | 1983-01-12 00:00:00 |
| JAMES  | 1981-12-03 00:00:00 |
| FORD   | 1981-12-03 00:00:00 |
| MILLER | 1982-01-23 00:00:00 |
+--------+---------------------+
9 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="3" %}
```
/*顯示薪資比公司平均薪資高的所有員工之員工編號，
姓名和薪資，並依薪資由高到低排列。*/
SELECT empno, ename, sal 
	FROM emp WHERE sal > (SELECT AVG(sal) 
													FROM emp) 
	ORDER BY sal DESC;
+-------+-------+---------+
| empno | ename | sal     |
+-------+-------+---------+
|  7839 | KING  | 5000.00 |
|  7788 | SCOTT | 3000.00 |
|  7902 | FORD  | 3000.00 |
|  7566 | JONES | 2975.00 |
|  7698 | BLAKE | 2850.00 |
|  7782 | CLARK | 2450.00 |
+-------+-------+---------+
6 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="4" %}
```
-- 顯示和姓名中包含T的人在相同部門工作的所有員工之員工編號和姓名。
SELECT deptno, ename 
		FROM emp 
    WHERE deptno IN (SELECT DISTINCT deptno 
							      FROM emp 
                    WHERE ename LIKE '%T%');
+--------+--------+
| deptno | ename  |
+--------+--------+
|     20 | SMITH  |
|     20 | JONES  |
|     20 | SCOTT  |
|     20 | ADAMS  |
|     20 | FORD   |
|     30 | ALLEN  |
|     30 | WARD   |
|     30 | MARTIN |
|     30 | BLAKE  |
|     30 | TURNER |
|     30 | JAMES  |
+--------+--------+
11 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="5" %}
```
-- 顯示和姓名中包含T的人在相同部門工作的所有員工之員工編號和姓名。
SELECT ename, deptno, job 
	FROM emp 
  WHERE deptno IN (SELECT deptno 
						       FROM dept 
                   WHERE LOC = 'Dallas');
+-------+--------+---------+
| ename | deptno | job     |
+-------+--------+---------+
| SMITH |     20 | CLERK   |
| JONES |     20 | MANAGER |
| SCOTT |     20 | ANALYST |
| ADAMS |     20 | CLERK   |
| FORD  |     20 | ANALYST |
+-------+--------+---------+
5 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="6" %}
```
-- 顯示直屬於"KING"的員工之姓名和薪資。
SELECT ename, sal 
	FROM emp 
  WHERE mgr = (SELECT empno 
					     FROM emp 
               WHERE ename='King');
+-------+---------+
| ename | sal     |
+-------+---------+
| JONES | 2975.00 |
| BLAKE | 2850.00 |
| CLARK | 2450.00 |
+-------+---------+
3 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="7" %}
```
-- 顯示銷售部門"SALES"所有員工之部門編號，姓名和職稱
SELECT deptno, ename, job 
		FROM emp 
    WHERE deptno = (SELECT deptno 
								    FROM dept 
                    WHERE dname='Sales');
+--------+--------+----------+
| deptno | ename  | job      |
+--------+--------+----------+
|     30 | ALLEN  | SALESMAN |
|     30 | WARD   | SALESMAN |
|     30 | MARTIN | SALESMAN |
|     30 | BLAKE  | MANAGER  |
|     30 | TURNER | SALESMAN |
|     30 | JAMES  | CLERK    |
+--------+--------+----------+
6 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="8" %}
```
/*顯示薪資比公司平均薪資還要高且和姓名中有T的人在相同部門上班的
所有員工之員工編號，姓名和薪資。*/
SELECT empno, ename, sal 
	FROM emp 
  WHERE deptno IN (SELECT DISTINCT deptno 
							   FROM emp 
                 WHERE ename LIKE '%T%' AND sal>(SELECT AVG(sal)
                                                   FROM emp));  
+-------+-------+---------+
| empno | ename | sal     |
+-------+-------+---------+
|  7369 | SMITH |  800.00 |
|  7566 | JONES | 2975.00 |
|  7788 | SCOTT | 3000.00 |
|  7876 | ADAMS | 1100.00 |
|  7902 | FORD  | 3000.00 |
+-------+-------+---------+
5 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="9" %}
```
/*顯示和賺取佣金的員工之部門編號和薪資都相同的員工之姓名，部門編號和薪資。*/
SELECT e1.ename, e1.deptno, e1.sal 
	FROM emp e1 JOIN (SELECT * FROM emp 
                     WHERE comm>0) e2 
						ON (e1.empno <> e2.empno 
								AND e1.deptno=e2.deptno 
								AND e1.sal = e2.sal);
+--------+--------+---------+
| ename  | deptno | sal     |
+--------+--------+---------+
| MARTIN |     30 | 1250.00 |
| WARD   |     30 | 1250.00 |
+--------+--------+---------+
2 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="10" %}
```
/*顯示和在DALLAS工作的員工之薪資和佣金相同的員工之姓名，部門編號和薪資。*/
SELECT e1.ename, e1.deptno, e1.sal 
	FROM emp e1 JOIN (SELECT * FROM emp 
                    WHERE deptno= (SELECT deptno
                   								FROM dept 
																	WHERE loc='Dallas')) e2 
						ON (e1.empno <> e2.empno 
								AND e1.sal = e2.sal 
								AND (e1.comm = e2.comm 
									OR (e1.comm IS NULL AND e2.comm is NULL)));
+-------+--------+---------+
| ename | deptno | sal     |
+-------+--------+---------+
| SCOTT |     20 | 3000.00 |
| FORD  |     20 | 3000.00 |
+-------+--------+---------+
2 rows in set (0.00 sec)
```
{% endtab %}

{% tab title="11" %}
```
/*顯示薪資和佣金都和SCOTT相同的所有員工之姓名，
進公司日期和薪資。(不要在結果中顯示SCOTT的資料)*/
SELECT e1.ename, e1.deptno, e1.sal 
	FROM emp e1 JOIN (SELECT * FROM emp 
										WHERE empno = (SELECT empno 
																	FROM emp 
																	WHERE ename='SCOTT')) e2 
						ON (e1.empno <> e2.empno 
						AND e1.sal = e2.sal 
						AND (e1.comm = e2.comm 
								OR (e1.comm IS NULL AND e2.comm is NULL)));
+-------+--------+---------+
| ename | deptno | sal     |
+-------+--------+---------+
| FORD  |     20 | 3000.00 |
+-------+--------+---------+
1 row in set (0.00 sec)
```
{% endtab %}

{% tab title="12" %}
```
/*顯示薪資比所有職稱是"CLERK"還高的員工之姓名，
進公司日期和薪資，並將結果依薪資由高志低顯示。*/
SELECT ename, hiredate, sal 
	FROM emp 
   WHERE sal > ALL (SELECT sal 
							      FROM emp
                    WHERE job = 'CLerk');
+--------+---------------------+---------+
| ename  | hiredate            | sal     |
+--------+---------------------+---------+
| ALLEN  | 1981-02-20 00:00:00 | 1600.00 |
| JONES  | 1981-04-02 00:00:00 | 2975.00 |
| BLAKE  | 1981-05-01 00:00:00 | 2850.00 |
| CLARK  | 1981-06-09 00:00:00 | 2450.00 |
| SCOTT  | 1982-12-09 00:00:00 | 3000.00 |
| KING   | 1981-11-17 00:00:00 | 5000.00 |
| TURNER | 1981-09-08 00:00:00 | 1500.00 |
| FORD   | 1981-12-03 00:00:00 | 3000.00 |
+--------+---------------------+---------+
8 rows in set (0.00 sec)
```
{% endtab %}
{% endtabs %}

