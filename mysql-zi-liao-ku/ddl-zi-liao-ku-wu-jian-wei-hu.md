---
description: 參照講義p.165 p.193
---

# DDL資料庫物件維護

## 新增物件CREATE  TABLE(p.167)

`CREATE TABLE [IF NOT EXISTS] 表格名稱`\
`(欄位名稱1 欄位型別1 [DEFAULT '預設值'][NOT NULL] [PRIMARY KEY],`\
&#x20;`欄位名稱2 欄位型別2,`\
&#x20;`...`\
&#x20;`欄位名稱n 欄位型別n,`\
`)[ENGINE 儲存引擎];`

{% tabs %}
{% tab title="First Tab" %}
```sql
CREATE TABLE IF NOT EXISTS dept               -- (p.169)
(    deptno SMALLINT(4) NOT NULL PRIMARY KEY, -- 欄位名 欄位型別 不為空值 主鍵
     dname VARCHAR(14) NOT NULL,
     Loc VAARCHAR(14) DEFAULT 'M',            -- 欄位名 欄位型別 預設值M
)ENGINE InnoDB;                               -- 儲存引擎InnoDB
```
{% endtab %}

{% tab title="Second Tab" %}
```sql
-- 「[CNSTRAINT 主鍵名稱] PRIMARY KEY(欄位名稱,...)」            -- 🔶【CNSTRAINT】
CREATE TABLE item12
(    ordid int not null,          -- 欄位名 欄位型別 不為空值
     itemid smallint not null,    -- 欄位名 欄位型別 不為空值
     CONSTRAINT pk_item_ordid_itemid PRIMARY KEY(ordid,itemid)-- 🔸複合主鍵
);
```

```sql
-- 「AUTO_INCREMENT」自動增加ex. 流水號            -- 【🔶AUTO_INCREMENT】
CREATE TABLE ord2
(    oredid INT AUTO_INCREMENT PRIMARY KEY,     -- 欄位名 欄位型別 自動增加 PK
     ord_date DATE,                             -- 欄位名 欄位型別
)AUTO_INCREMENT = 101;                          -- 🔸流水號起始碼
```

```sql
--「UNIQUE」唯一鍵      -- 🔶【UNIQUE】
CREATE TABLE emp
(...,
 VARCHAR(200) UNIQUE, -- 🔸
 ...,
);


-- 複合唯一鍵
CREATE TABLE item
( order INT NOT NULLk
  items SMALLINT NUT NULL,
  prodid smallint,
  CONSTRAINT uk_item_ordid_prodid UNIQUE(ordid,prodid)-- 🔸
);
```
{% endtab %}
{% endtabs %}

### 外來鍵FK (p.174)

* ON DELETE
* ON UPDATE

{% tabs %}
{% tab title="格式" %}
```
-- 新增
CREATE TABLE table
(...
    [CONSTRAINT 主鍵名]
    FOREIGN KEY(欄位名,...) REFERENCE 外來表格(外來表格欄)
);
```

```
/* 🔶RESTRICT 限制，
    子表有，附表就不准改
    例如，dept, deptno.10 -> 50 [X]不行改
    因為emp.deptno有10
*/
```
{% endtab %}

{% tab title="範例" %}
```sql
/* 🔶CASCADE 相依性
    父表刪子表一起刪
    例如，dept.deptno 10 -> delete
    emp.deptno 10 全刪
*/
CREATE TABLE t2           --🔹(p.10-23---p.176)
(fk SMALLINT,
 c2 CHAR(2),
 FOREIGN KEY(fk) REFERENCES t1(pk) ON DELETE CASCADE -- 🔸【ON DELETE CASCADE】
 -- 父子一起刪
);

/*---------------------------------------------------------------*/

CREATE TABLE t2           --🔹(p.10-25---p.177)
(fk SMALLINT,
 c2 CHAR(2),
 FOREIGN KEY(fk) REFERENCES t1(pk) ON UPDATE CASCADE -- 🔸【ON UPDATE CASCADE】
 -- 父子一起改
);
```

```sql
/* 🔶SET NULL 設成空值
    父表改，子表清成空值
    例如，dept.deptno 10 -> delete
    emp.deptno 10 -> Null
*/
CREATE TABLE t2           --🔹(p.10-24---p.176)
(fk SMALLINT,
 c2 CHAR(2),
 FOREIGN KEY(fk) REFERENCES t1(pk) ON DELETE SET NULL -- 🔸【ON DELETE SET NULL】
-- 父刪，子NULL
);

/*---------------------------------------------------------------*/

CREATE TABLE t2           --🔹(p.10-26---p.177)
(fk SMALLINT,
 c2 CHAR(2),
 FOREIGN KEY(fk) REFERENCES t1(pk) ON UPDATE SET NULL -- 🔸【ON UPDATE SET NULL 】
 -- 父改，子NULL
);
```
{% endtab %}
{% endtabs %}

### 使用現有資料建立新的資料表(p.178)

`CREATE TABLE 表格名[(欄位名)]`\
&#x20; `​AS`\
&#x20; `SELECT 欄位名`\
&#x20; `FROM 表格名`\
&#x20; `WHERE 條件`

{% tabs %}
{% tab title="使用現有資料建立新的資料表" %}
```sql
-- 用子查詢。用部分欄位建立新表格
CREATE TABLE emp10
  ​AS
  SELECT     empno,ename,job,sal
  FROM       emp
  WHERE      deptno = 10;

/*mysql> desc emp10;
+-------+--------------+------+-----+---------+-------+
| Field | Type         | Null | Key | Default | Extra |
+-------+--------------+------+-----+---------+-------+
| empno | int          | NO🔹 |     | NULL    |       |
| ename | varchar(10)  | YES  |     | NULL    |       |
| job   | varchar(9)   | YES  |     | NULL    |       |
| sal   | decimal(7,2) | YES  |     | NULL    |       |
+-------+--------------+------+-----+---------+-------+
4 rows in set (0.00 sec)*/
```
{% endtab %}

{% tab title="使用LIKE子句建立資料表" %}
* 使用LIKE子句建立新表格。
* 新表格**沒有任何資料**，表格是空的。
* 新表格的欄位、型態等（表頭）會被保留。

```
-- 建立                                (p.180)
mysql> create table emp1 like emp;
Query OK, 0 rows affected (0.13 sec)

-- 查詢🔸表頭
mysql> desc emp1;
+----------+--------------+------+-----+---------+-------+
| Field    | Type         | Null | Key | Default | Extra |
+----------+--------------+------+-----+---------+-------+
| EMPNO    | int          | NO   | PRI | NULL    |       |
| ENAME    | varchar(10)  | YES  |     | NULL    |       |
| JOB      | varchar(9)   | YES  |     | NULL    |       |
| MGR      | int          | YES  | MUL | NULL    |       |
| HIREDATE | datetime     | YES  |     | NULL    |       |
| SAL      | decimal(7,2) | YES  |     | NULL    |       |
| COMM     | decimal(7,2) | YES  |     | NULL    |       |
| DEPTNO   | int          | NO   | MUL | NULL    |       |
+----------+--------------+------+-----+---------+-------+

-- 查詢🔸沒有資料
mysql> select * from emp1;
Empty set (0.00 sec)
```
{% endtab %}
{% endtabs %}

## 修改物件ALTER  TABLE(欄位)(p.181)

`ALTER TABLE 表格名`\
`ADD | ALTER | MODIFY | CHANGE | DROP`

{% tabs %}
{% tab title="新增欄位(p.181)" %}
```sql
ALTER TABLE emp10
    ADD COLUMN mgr SMALLINT;
/*【🔹before】
mysql> desc emp10;
+-------+--------------+------+-----+---------+-------+
| Field | Type         | Null | Key | Default | Extra |
+-------+--------------+------+-----+---------+-------+
| empno | int          | NO   |     | NULL    |       |
| ename | varchar(10)  | YES  |     | NULL    |       |
| job   | varchar(9)   | YES  |     | NULL    |       |
| sal   | decimal(7,2) | YES  |     | NULL    |       |
+-------+--------------+------+-----+---------+-------+
4 rows in set (0.00 sec)*/

/*【🔹after】
mysql> desc emp10;
+-------+--------------+------+-----+---------+-------+
| Field | Type         | Null | Key | Default | Extra |
+-------+--------------+------+-----+---------+-------+
| empno | int          | NO   |     | NULL    |       |
| ename | varchar(10)  | YES  |     | NULL    |       |
| job   | varchar(9)   | YES  |     | NULL    |       |
| sal   | decimal(7,2) | YES  |     | NULL    |       |
| mgr🔹 | smallint     | YES  |     | NULL    |       |
+-------+--------------+------+-----+---------+-------+
5 rows in set (0.02 sec)*/
```
{% endtab %}

{% tab title="新增在第一欄(p.182)" %}
```sql
ALTER TABLE emp10
    ADD COLUMN phone VARCHAR(12) DEFAULT '02-66316710' FIRST; -- 🔶【FIRST】
/*【🔹before】
mysql> desc emp10;
+------------+--------------+------+-----+---------+-------+
| Field      | Type         | Null | Key | Default | Extra |
+------------+--------------+------+-----+---------+-------+
| empno      | int          | NO   |     | NULL    |       |
| ename      | varchar(10)  | YES  |     | NULL    |       |
| job        | varchar(9)   | YES  |     | NULL    |       |
| hiredate   | date         | YES  |     | NULL    |       |
| sal        | decimal(7,2) | YES  |     | NULL    |       |
| mgr        | smallint     | YES  |     | NULL    |       |
+------------+--------------+------+-----+---------+-------+
6 rows in set (0.00 sec)


【🔹after】
mysql> desc emp10;
+----------+--------------+------+-----+-------------+-------+
| Field    | Type         | Null | Key | Default     | Extra |
+----------+--------------+------+-----+-------------+-------+
| phone🔹  | varchar(12)  | YES  |     | 02-66316710 |       |
| empno    | int          | NO   |     | NULL        |       |
| ename    | varchar(10)  | YES  |     | NULL        |       |
| job      | varchar(9)   | YES  |     | NULL        |       |
| hiredate | date         | YES  |     | NULL        |       |
| sal      | decimal(7,2) | YES  |     | NULL        |       |
| mgr      | smallint     | YES  |     | NULL        |       |
+----------+--------------+------+-----+-------------+-------+
7 rows in set (0.00 sec)*/
```
{% endtab %}

{% tab title="新增指定欄位後(p.182)" %}
```sql
ALTER TABLE emp10                       -- 
    ADD COLUMN hiredate DATE AFTER job; -- 🔶【AFTER】
/*【🔹before】
mysql> desc emp10;
+-------+--------------+------+-----+---------+-------+
| Field | Type         | Null | Key | Default | Extra |
+-------+--------------+------+-----+---------+-------+
| empno | int          | NO   |     | NULL    |       |
| ename | varchar(10)  | YES  |     | NULL    |       |
| job   | varchar(9)   | YES  |     | NULL    |       |
| sal   | decimal(7,2) | YES  |     | NULL    |       |
| mgr   | smallint     | YES  |     | NULL    |       |
+-------+--------------+------+-----+---------+-------+
5 rows in set (0.02 sec)*/


/*【🔹after】
mysql> desc emp10;
+------------+--------------+------+-----+---------+-------+
| Field      | Type         | Null | Key | Default | Extra |
+------------+--------------+------+-----+---------+-------+
| empno      | int          | NO   |     | NULL    |       |
| ename      | varchar(10)  | YES  |     | NULL    |       |
| job        | varchar(9)   | YES  |     | NULL    |       |
| hiredate🔹 | date         | YES  |     | NULL    |       |
| sal        | decimal(7,2) | YES  |     | NULL    |       |
| mgr        | smallint     | YES  |     | NULL    |       |
+------------+--------------+------+-----+---------+-------+
6 rows in set (0.00 sec)*/
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="改欄位預設ALTER" %}
```sql
ALTER TABLE emp10            --(p.184)
ALTER phone DROP DEFAULT;

/*🔹【before】
mysql> desc emp10;
+----------+--------------+------+-----+---------------+-------+
| Field    | Type         | Null | Key | Default       | Extra |
+----------+--------------+------+-----+---------------+-------+
| phone    | varchar(12)  | YES  |     | 02-66316710🔹 |       |
| empno    | int          | NO   |     | NULL          |       |
| ename    | varchar(10)  | YES  |     | NULL          |       |
| job      | varchar(9)   | YES  |     | NULL          |       |
| hiredate | date         | YES  |     | NULL          |       |
| sal      | decimal(7,2) | YES  |     | NULL          |       |
| mgr      | smallint     | YES  |     | NULL          |       |
+----------+--------------+------+-----+---------------+-------+
7 rows in set (0.00 sec)

🔹【after】
mysql> desc emp10;
+----------+--------------+------+-----+---------+-------+
| Field    | Type         | Null | Key | Default | Extra |
+----------+--------------+------+-----+---------+-------+
| phone    | varchar(12)  | YES  |     | NULL🔹  |       |
| empno    | int          | NO   |     | NULL    |       |
| ename    | varchar(10)  | YES  |     | NULL    |       |
| job      | varchar(9)   | YES  |     | NULL    |       |
| hiredate | date         | YES  |     | NULL    |       |
| sal      | decimal(7,2) | YES  |     | NULL    |       |
| mgr      | smallint     | YES  |     | NULL    |       |
+----------+--------------+------+-----+---------+-------+
7 rows in set (0.00 sec)
*/
```
{% endtab %}

{% tab title="改欄位型態,順序MODIFY" %}
```sql
ALTER TABLE emp10                --(p.184)
MODIFY COLUMN mgr INT AFTER job; // 【INT】改型態了；【AFTER job】改位置了

/*🔹【before】
mysql> desc emp10;
+----------+--------------+------+-----+---------+-------+
| Field    | Type         | Null | Key | Default | Extra |
+----------+--------------+------+-----+---------+-------+
| phone    | varchar(12)  | YES  |     | NULL    |       |
| empno    | int          | NO   |     | NULL    |       |
| ename    | varchar(10)  | YES  |     | NULL    |       |
| job      | varchar(9)   | YES  |     | NULL    |       |
| hiredate | date         | YES  |     | NULL    |       |
| sal      | decimal(7,2) | YES  |     | NULL    |       |
| 🟡mgr    | smallint🔹   | YES  |     | NULL    |       |
+----------+--------------+------+-----+---------+-------+
7 rows in set (0.00 sec)

🔹【after】
mysql> desc emp10;
+----------+--------------+------+-----+---------+-------+
| Field    | Type         | Null | Key | Default | Extra |
+----------+--------------+------+-----+---------+-------+
| phone    | varchar(12)  | YES  |     | NULL    |       |
| empno    | int          | NO   |     | NULL    |       |
| ename    | varchar(10)  | YES  |     | NULL    |       |
| job      | varchar(9)   | YES  |     | NULL    |       |
|🟡 mgr    | int🔹        | YES  |     | NULL    |       |
| hiredate | date         | YES  |     | NULL    |       |
| sal      | decimal(7,2) | YES  |     | NULL    |       |
+----------+--------------+------+-----+---------+-------+
7 rows in set (0.00 sec)
*/
```
{% endtab %}

{% tab title="改欄位型態MODIFY" %}
```sql
ALTER TABLE emp                            -- (p.185)
MODIFY COLUMN ename VARCHAR(10) NOT NULL;
/*🔹【before】
mysql> desc emp10;
+----------+--------------+------+-----+---------+-------+
| Field    | Type         | Null | Key | Default | Extra |
+----------+--------------+------+-----+---------+-------+
| phone    | varchar(12)  | YES  |     | NULL    |       |
| empno    | int          | NO   |     | NULL    |       |
| ename    | varchar(10)🔹| YES  |     | NULL🔹  |       |
| job      | varchar(9)   | YES  |     | NULL    |       |
| mgr      | int          | YES  |     | NULL    |       |
| hiredate | date         | YES  |     | NULL    |       |
| sal      | decimal(7,2) | YES  |     | NULL    |       |
+----------+--------------+------+-----+---------+-------+
7 rows in set (0.00 sec)

🔹【after】 == 原本就一樣.........
mysql> desc emp10;
+----------+--------------+------+-----+---------+-------+
| Field    | Type         | Null | Key | Default | Extra |
+----------+--------------+------+-----+---------+-------+
| phone    | varchar(12)  | YES  |     | NULL    |       |
| empno    | int          | NO   |     | NULL    |       |
| ename    | varchar(10)🔹| YES  |     | NULL🔹  |       |
| job      | varchar(9)   | YES  |     | NULL    |       |
| mgr      | int          | YES  |     | NULL    |       |
| hiredate | date         | YES  |     | NULL    |       |
| sal      | decimal(7,2) | YES  |     | NULL    |       |
+----------+--------------+------+-----+---------+-------+
7 rows in set (0.00 sec)
*/
```
{% endtab %}

{% tab title="更改欄位名稱、型態CHANGE" %}
```sql
ALTER TABLE emp10                        -- (p.186)
CHANGE COLUMN sal salary SMALLINT;
/*🔹【before】
mysql> desc emp10;
+----------+--------------+------+-----+---------+-------+
| Field    | Type         | Null | Key | Default | Extra |
+----------+--------------+------+-----+---------+-------+
| phone    | varchar(12)  | YES  |     | NULL    |       |
| empno    | int          | NO   |     | NULL    |       |
| ename    | varchar(10)  | YES  |     | NULL    |       |
| job      | varchar(9)   | YES  |     | NULL    |       |
| mgr      | int          | YES  |     | NULL    |       |
| hiredate | date         | YES  |     | NULL    |       |
| 🟡sal    | decimal(7,2) | YES  |     | NULL    |       |
+----------+--------------+------+-----+---------+-------+
7 rows in set (0.00 sec)

🔹【after】
mysql> desc emp10;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| phone    | varchar(12) | YES  |     | NULL    |       |
| empno    | int         | NO   |     | NULL    |       |
| ename    | varchar(10) | YES  |     | NULL    |       |
| job      | varchar(9)  | YES  |     | NULL    |       |
| mgr      | int         | YES  |     | NULL    |       |
| hiredate | date        | YES  |     | NULL    |       |
|🟡salary  | smallint    | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
7 rows in set (0.00 sec)
*/
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
CHANGE 與 MODIFY相似，\
CHANGE可以重新命名；MODIFY不能重新命名。
{% endhint %}

## 刪除物件DROP  TABLE

| 刪除欄位(表格在、資料不在)                                                    | 刪除資料表(表格不在)      |
| ----------------------------------------------------------------- | ---------------- |
| <p><code>ALTER TABLE 表格名</code><br><code>DROP [COLUMN]</code></p> | `DROP TABLE 表格名` |

{% tabs %}
{% tab title="刪除欄位" %}
```sql
ALTER TABLE dpt1            --(p.186)
DROP COLUMN loc;

/*🔹【before】
mysql> desc dept1;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| DEPTNO | int         | NO   |     | NULL    |       |
| DNAME  | varchar(14) | YES  |     | NULL    |       |
| 🟡LOC  | varchar(13) | YES  |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
3 rows in set (0.08 sec)


🔹【after】
mysql> desc dept1;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| DEPTNO | int         | NO   |     | NULL    |       |
| DNAME  | varchar(14) | YES  |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
2 rows in set (0.00 sec)
*/
```
{% endtab %}

{% tab title="刪除資料表" %}
```sql
DROP TABLE emp10a;
```
{% endtab %}
{% endtabs %}

## 視觀表view

* 虛擬資料表，本身不儲存任何資料。
* 特性：
  * 可加強安全性。檢視表可以設定唯讀
  * 簡化查詢複雜度
  * 結構變更時，可以改view設定不需要改程式。
  * 一資料表可建立多視觀表

{% tabs %}
{% tab title="建立視觀表" %}
語法：`CREATE [OR REPLACE] VIEW column`\
`AS <select_statement>`「or replace」是選填。

* 加上「or replace」，當有同名的view存在時，覆蓋它(alter view)。
* 加上「or replace」，當沒有同名的view存在時，建立一個(create view)。

### 建立視觀表

```sql
mysql> CREATE VIEW empvu10
    -> AS
    ->   SELECT *
    ->   FROM  emp
    ->   WHERE deptno = 10;
Query OK, 0 rows affected (0.17 sec)

mysql> SELECT * FROM empvu10;
/*
+-------+--------+-----------+------+---------------------+---------+------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE            | SAL     | COMM | DEPTNO |
+-------+--------+-----------+------+---------------------+---------+------+--------+
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 00:00:00 | 2450.00 | NULL |     10 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 00:00:00 | 5000.00 | NULL |     10 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 00:00:00 | 1300.00 | NULL |     10 |
+-------+--------+-----------+------+---------------------+---------+------+--------+
3 rows in set (0.03 sec)*/
```

### 建立視觀表－設定欄位名稱

```sql
mysql> CREATE VIEW salvu20 (employee_no, employee, annual_sal)
    -> AS
    -> SELECT empno, ename, sal*12
    -> FROM emp
    -> WHERE deptno = 20;
Query OK, 0 rows affected (0.02 sec)

mysql> SELECT * FROM salvu20;/*
+-------------+----------+------------+
| employee_no | employee | annual_sal |
+-------------+----------+------------+
|        7369 | SMITH    |    9600.00 |
|        7566 | JONES    |   35700.00 |
|        7788 | SCOTT    |   36000.00 |
|        7876 | ADAMS    |   13200.00 |
|        7902 | FORD     |   36000.00 |
+-------------+----------+------------+
5 rows in set (0.00 sec)*/
```

### 建立視觀表－設定欄位名稱(別名)

```sql
mysql> CREATE VIEW salvu30
    -> AS
    -> SELECT empno 'employee_number', ename 'name', sal 'salary'
    -> FROM emp
    -> WHERE deptno = 30;
Query OK, 0 rows affected (0.01 sec)

mysql> SELECT * FROM salvu30;/*
+-----------------+--------+---------+
| employee_number | name   | salary  |
+-----------------+--------+---------+
|            7499 | ALLEN  | 1600.00 |
|            7521 | WARD   | 1250.00 |
|            7654 | MARTIN | 1250.00 |
|            7698 | BLAKE  | 2850.00 |
|            7844 | TURNER | 1500.00 |
|            7900 | JAMES  |  950.00 |
+-----------------+--------+---------+
6 rows in set (0.00 sec)*/
```
{% endtab %}

{% tab title="建立複雜視觀表" %}
JOIN ON

```sql
mysql> CREATE VIEW dept_sum_vu(name, minsal, maxsal, avgsal)
    -> AS
    -> SELECT d.dname, MIN(e.sal), MAX(e.sal), AVG(e.sal)
    -> FROM emp e JOIN dept d ON(e.deptno = d.deptno)
    -> GROUP BY d.dname;
/*Query OK, 0 rows affected (0.03 sec)*/

mysql> DESC dept_sum_vu;/*
+--------+---------------+------+-----+---------+-------+
| Field  | Type          | Null | Key | Default | Extra |
+--------+---------------+------+-----+---------+-------+
| name   | varchar(14)   | YES  |     | NULL    |       |
| minsal | decimal(7,2)  | YES  |     | NULL    |       |
| maxsal | decimal(7,2)  | YES  |     | NULL    |       |
| avgsal | decimal(11,6) | YES  |     | NULL    |       |
+--------+---------------+------+-----+---------+-------+
4 rows in set (0.01 sec)*/

mysql>     SELECT * FROM dept_sum_vu;/*
+------------+---------+---------+-------------+
| name       | minsal  | maxsal  | avgsal      |
+------------+---------+---------+-------------+
| ACCOUNTING | 1300.00 | 5000.00 | 2916.666667 |
| RESEARCH   |  800.00 | 3000.00 | 2175.000000 |
| SALES      |  950.00 | 2850.00 | 1566.666667 |
+------------+---------+---------+-------------+
3 rows in set (0.00 sec)*/
```
{% endtab %}

{% tab title="查詢" %}
查詢功能與資料表完全一樣

```sql
mysql> SELECT COUNT(*),SUM(salary) 'sum_sal_30',AVG(salary) 'avg_sal_30'
    -> FROM salvu30;/*
+----------+------------+-------------+
| COUNT(*) | sum_sal_30 | avg_sal_30  |
+----------+------------+-------------+
|        6 |    9400.00 | 1566.666667 |
+----------+------------+-------------+
1 row in set (0.00 sec)*/

mysql> SELECT name, avgsal
    -> FROM dept_sum_vu
    -> WHERE avgsal>2000;/*
+------------+-------------+
| name       | avgsal      |
+------------+-------------+
| ACCOUNTING | 2916.666667 |
| RESEARCH   | 2175.000000 |
+------------+-------------+
2 rows in set (0.00 sec)*/
```
{% endtab %}

{% tab title="更新" %}
### 查詢view是否可執行DML命令

```sql
mysql> SELECT TABLE_NAME, IS_UPDATABLE
    -> FROM information_schema.views;/*
+-----------------------------------------------+--------------+
| TABLE_NAME                                    | IS_UPDATABLE |
+-----------------------------------------------+--------------+
| film_list                                     | NO           |
| nicer_but_slower_film_list                    | NO           |
| staff_list                                    | YES          |
| sales_by_store                                | NO           |
| sales_by_film_category                        | NO           |
| actor_info                                    | NO           |
| empvu10                                       | YES          |
| salvu20                                       | YES          |
| salvu30                                       | YES          |
| dept_sum_vu                                   | NO           |
+-----------------------------------------------+--------------+
*/
```

### 視觀表－資料更新

```sql
mysql> UPDATE salvu30
    -> SET salary = 2000
    -> WHERE employee_number=7499;
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

/*🔹查詢視觀表內容
mysql> SELECT * FROM salvu30;
+-----------------+--------+---------+
| employee_number | name   | salary  |
+-----------------+--------+---------+
|            7499 | ALLEN  | 2000.00 |
|            7521 | WARD   | 1250.00 |
|            7654 | MARTIN | 1250.00 |
|            7698 | BLAKE  | 2850.00 |
|            7844 | TURNER | 1500.00 |
|            7900 | JAMES  |  950.00 |
+-----------------+--------+---------+
6 rows in set (0.00 sec)*/

/*🔹查詢基底資料表
mysql> SELECT empno, ename, job, sal
    ->     FROM emp
    ->     WHERE empno=7499;
+-------+-------+----------+---------+
| empno | ename | job      | sal     |
+-------+-------+----------+---------+
|  7499 | ALLEN | SALESMAN | 2000.00 |
+-------+-------+----------+---------+
1 row in set (0.00 sec)*/
```

### 視觀表－可更新與不可更新

&#x20;\*基底資料表-非計算欄位，view可更新\
&#x20;\*基底資料表-的計算欄位，view不可更新&#x20;

```sql
 -- 🟡可更新的資料
mysql>  UPDATE salvu20
    ->  SET employee='mary'
    ->  WHERE employee_no=7902;
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

/*🔹查詢視觀表
mysql> SELECT * FROM salvu20;
+-------------+----------+------------+
| employee_no | employee | annual_sal |
+-------------+----------+------------+
|        7369 | SMITH    |    9600.00 |
|        7566 | JONES    |   35700.00 |
|        7788 | SCOTT    |   36000.00 |
|        7876 | ADAMS    |   13200.00 |
|      🔸7902 | mary     |   36000.00 |
+-------------+----------+------------+
5 rows in set (0.01 sec)*/

 -- 🟡不可更新的資料👇當初[annual_sal]是emp*12得來的計算欄位，view是無法更新的。
mysql>  UPDATE salvu20
    ->  SET annual_sal=48000
    ->  WHERE employee_no=7902;
ERROR 1348 (HY000): Column 'annual_sal' is not updatable
```
{% endtab %}

{% tab title="新增" %}
### 新增資料

```sql
mysql> INSERT INTO empvu10(empno,ename,sal ,deptno)
    -> VALUES(9700,'KEN',3800,10);
Query OK, 1 row affected (0.01 sec)

/*mysql> SELECT * FROM empvu10;
+-------+--------+-----------+------+---------------------+---------+------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE            | SAL     | COMM | DEPTNO |
+-------+--------+-----------+------+---------------------+---------+------+--------+
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 00:00:00 | 2450.00 | NULL |     10 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 00:00:00 | 5000.00 | NULL |     10 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 00:00:00 | 1300.00 | NULL |     10 |
|  9700 | KEN    | NULL      | NULL | NULL                | 3800.00 | NULL |     10 |
+-------+--------+-----------+------+---------------------+---------+------+--------+
4 rows in set (0.00 sec)*/
```

### -- 跟資料更新一樣，計算欄位一樣不能新增P.11-17

```sql
/*mysql> DESC emp;
+----------+--------------+------+-----+---------+-------+
| Field    | Type         | Null | Key | Default | Extra |
+----------+--------------+------+-----+---------+-------+
| EMPNO    | int          | NO   | PRI | NULL    |       |
| ENAME    | varchar(10)  | YES  |     | NULL    |       |
| JOB      | varchar(9)   | YES  |     | NULL    |       |
| MGR      | int          | YES  | MUL | NULL    |       |
| HIREDATE | datetime     | YES  |     | NULL    |       |
| SAL      | decimal(7,2) | YES  |     | NULL    |       |
| COMM     | decimal(7,2) | YES  |     | NULL    |       |
| DEPTNO   | int          | NO   | MUL | NULL    |       |
+----------+--------------+------+-----+---------+-------+
8 rows in set (0.02 sec)*/

mysql> INSERT INTO salvu20
    -> VALUES(9800,'JACKSON',24000);
/*ERROR 1348 (HY000): Column 'annual_sal' is not updatable*/
```
{% endtab %}

{% tab title="刪除" %}
### 刪除資料

```sql
mysql> DELETE FROM empvu10
    -> WHERE empno=9700;
--Query OK, 1 row affected (0.01 sec)

mysql> DELETE FROM salvu30
    -> WHERE name='james';
--Query OK, 1 row affected (0.01 sec)
```

### 無法刪除－違反基底資料表的資料檢查條件

```sql
/*mysql>  SELECT * FROM salvu20;
+-------------+----------+------------+
| employee_no | employee | annual_sal |
+-------------+----------+------------+
|        7369 | SMITH    |    9600.00 |
|        7566 | JONES    |   35700.00 |
|        7788 | SCOTT    |   36000.00 |
|        7876 | ADAMS    |   13200.00 |
|        7902 | mary     |   36000.00 |
+-------------+----------+------------+
5 rows in set (0.00 sec)*/

mysql>  DELETE FROM salvu20
    ->  WHERE employee_no='7902';
/*ERROR 1451 (23000): Cannot delete or update a parent row: 
a foreign key constraint fails (`demo`.`emp`, CONSTRAINT `EMP_MGR_FK` FOREIGN KEY (`MGR`) REFERENCES `emp` (`EMPNO`))*/
```

### &#x20;複雜視觀表－無法做DML p.11-19

```sql
/*mysql> SELECT * FROM dept_sum_vu;
+------------+---------+---------+-------------+
| name       | minsal  | maxsal  | avgsal      |
+------------+---------+---------+-------------+
| ACCOUNTING | 1300.00 | 5000.00 | 2916.666667 |
| RESEARCH   |  800.00 | 3000.00 | 2175.000000 |
| SALES      | 1250.00 | 2850.00 | 1770.000000 |
+------------+---------+---------+-------------+
3 rows in set (0.00 sec)*/

mysql> INSERT INTO dept_sum_vu
    -> VALUES('education',1200,3000,2800);
--ERROR 1471 (HY000): The target table dept_sum_vu of the INSERT is not insertable-into

mysql> UPDATE dept_sum_vu
    -> SET maxsal=4800
    -> WHERE name='sales';
--ERROR 1288 (HY000): The target table dept_sum_vu of the UPDATE is not updatable

mysql> DELETE FROM dept_sum_vu
    -> WHERE name='research';
--ERROR 1288 (HY000): The target table dept_sum_vu of the DELETE is not updatable
```
{% endtab %}

{% tab title="修改" %}
### 修改視觀表內容

\-- 增加「WHITH CHECK OPTION」選項，違反VIEW的條件就不能修改。

```sql
mysql> ALTER VIEW salvu30
    -> AS
    -> SELECT empno 'employee_number',ename 'name',sal 'salary',deptno
    -> FROM emp
    -> WHERE deptno = 30
    -> WITH CHECK OPTION;-- 🟡
--Query OK, 0 rows affected (0.03 sec)

/*mysql> SELECT * FROM salvu30;
+-----------------+--------+---------+--------+
| employee_number | name   | salary  | deptno |
+-----------------+--------+---------+--------+
|            7499 | ALLEN  | 2000.00 |     30 |
|            7521 | WARD   | 1250.00 |     30 |
|            7654 | MARTIN | 1250.00 |     30 |
|            7698 | BLAKE  | 2850.00 |     30 |
|            7844 | TURNER | 1500.00 |     30 |
+-----------------+--------+---------+--------+
5 rows in set (0.02 sec)*/
```

### with check option選項－－可執行

```sql
/*mysql> SELECT * FROM salvu30;
+-----------------+--------+---------+--------+
| employee_number | name   | salary  | deptno |
+-----------------+--------+---------+--------+
|            7499 | ALLEN  | 2000.00 |     30 |
|            7521 | WARD   | 1250.00 |     30 |
|            7654 | MARTIN | 1250.00 |     30 |
|            7698 | BLAKE  | 2850.00 |     30 |
|            7844 | TURNER | 1500.00 |     30 |
+-----------------+--------+---------+--------+
5 rows in set (0.02 sec)*/

mysql> UPDATE salvu30
    -> SET salary = 2000
    -> WHERE employee_number=7499;
--Query OK, 0 rows affected (0.01 sec)
--Rows matched: 1  Changed: 0  Warnings: 0

mysql> DELETE FROM salvu30 WHERE employee_number=7521;
--Query OK, 1 row affected (0.01 sec)
```

### with check option選項－－不可執行

```sql
/*mysql> SELECT * FROM salvu30;
+-----------------+--------+---------+--------+
| employee_number | name   | salary  | deptno |🔸部門編號view是抓30
+-----------------+--------+---------+--------+
|            7499 | ALLEN  | 2000.00 |     30 |
|            7521 | WARD   | 1250.00 |     30 |
|            7654 | MARTIN | 1250.00 |     30 |
|            7698 | BLAKE  | 2850.00 |     30 |
|            7844 | TURNER | 1500.00 |     30 |
+-----------------+--------+---------+--------+
5 rows in set (0.02 sec)*/

-- 不可違反where子句的條件
mysql> UPDATE salvu30
    -> SET deptno = 10                        --🔸部門編號view沒有10
    -> WHERE employee_number=7499;
--ERROR 1369 (HY000): CHECK OPTION failed 'demo.salvu30'
```
{% endtab %}

{% tab title="刪除視觀表" %}
\-- 從資料庫中刪除視觀表，不會刪除任何(基底)資料

```sql
mysql> DROP VIEW dept_sum_vu;
--Query OK, 0 rows affected (0.04 sec)
```
{% endtab %}

{% tab title="內嵌視觀表" %}
.

```sql
mysql> SELECT a.ename, a.sal, a.deptno, b.avgsal
    -> FROM   emp a JOIN(SELECT deptno, AVG(sal) avgsal
    ->                   FROM emp
    ->                   GROUP BY deptno) b
    ->               ON (a.deptno = b.deptno)
    -> WHERE  a.sal < b.avgsal;/*
+--------+---------+--------+-------------+
| ename  | sal     | deptno | avgsal      |
+--------+---------+--------+-------------+
| SMITH  |  800.00 |     20 | 2175.000000 |
| MARTIN | 1250.00 |     30 | 1900.000000 |
| CLARK  | 2450.00 |     10 | 2916.666667 |
| TURNER | 1500.00 |     30 | 1900.000000 |
| ADAMS  | 1100.00 |     20 | 2175.000000 |
| MILLER | 1300.00 |     10 | 2916.666667 |
+--------+---------+--------+-------------+
6 rows in set (0.00 sec)*/
```
{% endtab %}
{% endtabs %}



## 索引index

p.205

## 作業練習－DDL(p.191)

1.  用下列資料新建DEPARTMENT資料表\
    `column name	null?		data type`

    `id		NOT NULL	NUMERIC(7)`

    `name		NOT NULL	VARCHAR(24)`
2. 利用DEPT資料表，將資料新增至DEPARTMENT資料表中(只新增相對的資料欄)
3.  利用下列資料新建EMPLOYEE資料表\
    `column name	Null?		data Type`

    `id		NOT NULL	NUM*ERIC(7)`

    `last_nam*e	NOT NULL	VARCHAR(24)`

    `first_name		 	VARCHAR(24)`

    `dept_id	 			NUMERIC(7)`
4. 將EMPLOYEE資料表中last\_name欄位資料型態更改為varchar(40)
5. 使用EMP資料表結構中EMPNO,ENAME, DEPTNO定義來新建EMPLOYEE2資料表\
   並將欄位名稱設定為id, last\_name,dept\_id
6. 刪除整個EMPLOYEE資料表
7. 將EMPLOYEE2資料表改名為EMPLOYEE
8. 將EMPLOYEE資料表中的LAST\_NAME欄位刪除
9. 修改EMPLOYEE資料表，新增一個欄位SALARY資料型態為NUMERIC , precision 7
10. 修改EMPLOYEE資料表，使用ID欄位新增一個primary key限制條件，並為他命名
11. 在EMPLOYEE資料表新增一個外部鍵(foreign key)以確保員工不會被分派到一個不存在的部門。

{% tabs %}
{% tab title="1" %}
```
/*用下列資料新建DEPARTMENT資料表
column name	null?		data type
id		NOT NULL	NUMERIC(7)
name		NOT NULL	VARCHAR(24)*/

CREATE TABLE department 
	(id NUMERIC(7) NOT NULL, 
	 name VARCHAR(24) NOT NULL); 
```
{% endtab %}

{% tab title="2" %}
```
-- 利用DEPT資料表，將資料新增至DEPARTMENT資料表中(只新增相對的資料欄)
INSERT INTO department(id, name) 
	SELECT deptno, dname FROM dept;
```
{% endtab %}

{% tab title="3" %}
```
/*利用下列資料新建EMPLOYEE資料表
column name	Null?		data Type
id		NOT NULL	NUMERIC(7)
last_name	NOT NULL	VARCHAR(24)
first_name		 	VARCHAR(24)
dept_id	 			NUMERIC(7)*/

CREATE TABLE employee 
	(id NUMERIC(7) NOT NULL, 
     last_name VARCHAR(24) NOT NULL, 
     frist_name VARCHAR(24), 
     deptno NUMERIC(7)); 
```
{% endtab %}

{% tab title="4" %}
```
-- 將EMPLOYEE資料表中last_name欄位資料型態更改為varchar(40)
ALTER TABLE employee 
	CHANGE COLUMN last_name last_name VARCHAR(40);

```
{% endtab %}

{% tab title="5" %}
```
/*使用EMP資料表結構中EMPNO,ENAME, DEPTNO定義來新建EMPLOYEE2資料表
並將欄位名稱設定為id, last_name,dept_id*/


CREATE TABLE employee2 
	SELECT empno AS id, 
		   ename AS last_name, 
           deptno AS dept_id 
	FROM emp;
```
{% endtab %}

{% tab title="6" %}
```
-- 刪除整個EMPLOYEE資料表
DROP TABLE employee;
```
{% endtab %}

{% tab title="7" %}
```
-- 將EMPLOYEE2資料表改名為EMPLOYEE
ALTER TABLE employee2 
	RENAME AS employee;

```
{% endtab %}

{% tab title="8" %}
```
-- 將EMPLOYEE資料表中的LAST_NAME欄位刪除
ALTER TABLE employee 
	DROP last_name;
```
{% endtab %}

{% tab title="9" %}
```
-- 修改EMPLOYEE資料表，新增一個欄位SALARY資料型態為NUMERIC , precision 7
ALTER TABLE employee 
	ADD salary NUMERIC(7);
```
{% endtab %}

{% tab title="10" %}
```
-- 修改EMPLOYEE資料表，使用ID欄位新增一個primary key限制條件，並為他命名
ALTER TABLE employee 
	ADD CONSTRAINT pk_employee_id PRIMARY KEY(id);
```
{% endtab %}

{% tab title="11" %}
```
-- 在EMPLOYEE資料表新增一個外部鍵(foreign key)以確保員工不會被分派到一個不存在的部門。

ALTER TABLE employee 
ADD CONSTRAINT fk_employee_deptid FOREIGN KEY(dept_id) REFERENCES dept(deptno);
```
{% endtab %}
{% endtabs %}

## 作業練習－DDL-view(p.208)

1. 使用EMP資料表中員編、姓名、部門編號 建立一個EMP\_VU view，並將姓名欄改以EMPLOYEE
2. 顯示EMP\_VU view中的資料內容
3. 使用EMP\_VU view來顯示所有員工姓名及部門編號。
4. 新建一個名為DEPT20的view，包含部門20的所有員工編號、姓名、部門編號。將view資料項目命名為employee\_id, employee, department\_id，並設定不允許使用者透過DEPT20來更改員工所屬部門編號。
5. 顯示DEPT20 view欄位定義資料(結構)及其所有資料內容。
6. 試試看利用DEPT20 view將Smith轉調到部門30
7. 新建一個名為SALARY\_VU的view，包含所有員工姓名、部門名稱、薪資、薪資等級。\
   將view中的資料項目分別命名為employee,department,salary,grade\


{% tabs %}
{% tab title="1" %}
```
-- 使用EMP資料表中員編、姓名、部門編號 建立一個EMP_VU view，並將姓名欄改以EMPLOYEE

```
{% endtab %}

{% tab title="2" %}
```
-- 顯示EMP_VU view中的資料內容

```
{% endtab %}

{% tab title="3" %}
```
-- 使用EMP_VU view來顯示所有員工姓名及部門編號。

```
{% endtab %}

{% tab title="4" %}
```
/*新建一個名為DEPT20的view，包含部門20的所有員工編號、姓名、部門編號。
將view資料項目命名為employee_id, employee, department_id，
並設定不允許使用者透過DEPT20來更改員工所屬部門編號。*/

```
{% endtab %}

{% tab title="5" %}
```
-- 顯示DEPT20 view欄位定義資料(結構)及其所有資料內容。

```
{% endtab %}

{% tab title="6" %}
```
-- 試試看利用DEPT20 view將Smith轉調到部門30

```
{% endtab %}

{% tab title="7" %}
```
/*新建一個名為SALARY_VU的view，包含所有員工姓名、部門名稱、薪資、薪資等級。
將view中的資料項目分別命名為employee,department,salary,grade*/

```
{% endtab %}
{% endtabs %}
