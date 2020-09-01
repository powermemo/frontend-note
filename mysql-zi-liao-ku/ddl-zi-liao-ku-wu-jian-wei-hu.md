---
description: 參照講義p.165 p.193
---

# DDL資料庫物件維護

## 新增物件

`CREATE TABLE [IF NOT EXISTS] 表格名稱  
(欄位名稱1 欄位型別1 [DEFAULT '預設值'][NOT NULL] [PRIMARY KEY],  
 欄位名稱2 欄位型別2,  
 ...  
 欄位名稱n 欄位型別n,  
)[ENGINE 儲存引擎];`

```sql
CREATE TABLE IF NOT EXISTS dept
(    deptno SMALLINT(4) NOT NULL PRIMARY KEY, -- 欄位名 欄位型別 不為空值 主鍵
     dname VARCHAR(14) NOT NULL,
     Loc VAARCHAR(14) DEFAULT 'M',            -- 欄位名 欄位型別 預設值M
)ENGINE InnoDB;                               -- 儲存引擎InnoDB
```

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

### 外來鍵FK

* ON DELETE
* ON UPDATE

```text
-- 新增
CREATE TABLE table
(...
    [CONSTRAINT 主鍵名]
        FOREIGN KEY(欄位名,...) REFERENCE 外來表格(外來表格欄)
);
```

```text
/* 🔶RESTRICT 限制，
    子表有，附表就不准改
    例如，dept, deptno.10 -> 50 [X]不行改
    因為emp.deptno有10
*/
```

```sql
/* 🔶CASCADE 相依性
    父表刪子表一起刪
    例如，dept.deptno 10 -> delete
    emp.deptno 10 全刪
*/
CREATE TABLE t2
(fk SMALLINT,
 c2 CHAR(2),
 FOREIGN KEY(fk) REFERENCES t1(pk) ON DELETE CASCADE -- 🔸【ON DELETE CASCADE 】
 -- 父子一起刪
);

/*---------------------------------------------------------------*/

CREATE TABLE t2
(fk SMALLINT,
 c2 CHAR(2),
 FOREIGN KEY(fk) REFERENCES t1(pk) ON UPDATE CASCADE -- 🔸【ON UPDATE CASCADE 】
 -- 父子一起改
);
```

```sql
/* 🔶SET NULL 設成空值
    父表改，子表清成空值
    例如，dept.deptno 10 -> delete
    emp.deptno 10 -> Null
*/
CREATE TABLE t2
(fk SMALLINT,
 c2 CHAR(2),
 FOREIGN KEY(fk) REFERENCES t1(pk) ON DELETE SET NULL -- 🔸【ON DELETE SET NULL】
-- 父刪，子NULL
);

/*---------------------------------------------------------------*/

CREATE TABLE t2
(fk SMALLINT,
 c2 CHAR(2),
 FOREIGN KEY(fk) REFERENCES t1(pk) ON UPDATE SET NULL -- 🔸【ON UPDATE SET NULL 】
 -- 父改，子NULL
);
```

### 使用現有資料建立新的資料表

`CREATE TABLE 表格名[(欄位名)]  
  ​AS  
  SELECT 欄位名  
  FROM 表格名  
  WHERE 條件`

```sql
-- 用子查詢
CREATE TABLE emp10
  ​AS
  SELECT empno,ename,job,sal
  FROM emp
  WHERE deptno = 10;

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

### 新增欄位

`ALTER TABLE 表格名  
ADD | ALTER | MODIFY | CHANGE | DROP`

{% tabs %}
{% tab title="新增" %}
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

{% tab title="新增在第一欄" %}
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

{% tab title="新增指定欄位後" %}
```sql
ALTER TABLE emp10
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

## 修改物件

`ALTER TABLE 表格名  
ALTER | MODIFY | CHANGE`

{% tabs %}
{% tab title="改欄位預設" %}
```sql
ALTER TABLE emp10
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

{% tab title="改欄位型態,順序" %}
```sql
ALTER TABLE emp10
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

{% tab title="改欄位型態" %}
```sql
ALTER TABLE emp
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

{% tab title="更改欄位名稱、型態" %}
```sql
ALTER TABLE emp10
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
CHANGE 與 MODIFY相似，  
CHANGE可以重新命名；MODIFY不能重新命名。
{% endhint %}

## 刪除物件

| 刪除欄位 | 刪除資料表 |
| :--- | :--- |
| `ALTER TABLE 表格名 DROP [COLUMN]` | `DROP TABLE 表格名` |

{% tabs %}
{% tab title="刪除欄位" %}
```sql
ALTER TABLE dpt1
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

### 建立視觀表

## 作業練習－DDL\(p.191\)

1. 用下列資料新建DEPARTMENT資料表  
   `column name	null?		data type`

   `id		NOT NULL	NUMERIC(7)`

   `name		NOT NULL	VARCHAR(24)`

2. 利用DEPT資料表，將資料新增至DEPARTMENT資料表中\(只新增相對的資料欄\)
3. 利用下列資料新建EMPLOYEE資料表  
   `column name	Null?		data Type`

   `id		NOT NULL	NUM*ERIC(7)`

   `last_nam*e	NOT NULL	VARCHAR(24)`

   `first_name		 	VARCHAR(24)`

   `dept_id	 			NUMERIC(7)`

4. 將EMPLOYEE資料表中last\_name欄位資料型態更改為varchar\(40\)
5. 使用EMP資料表結構中EMPNO,ENAME, DEPTNO定義來新建EMPLOYEE2資料表 並將欄位名稱設定為id, last\_name,dept\_id
6. 刪除整個EMPLOYEE資料表
7. 將EMPLOYEE2資料表改名為EMPLOYEE
8. 將EMPLOYEE資料表中的LAST\_NAME欄位刪除
9. 修改EMPLOYEE資料表，新增一個欄位SALARY資料型態為NUMERIC , precision 7
10. 修改EMPLOYEE資料表，使用ID欄位新增一個primary key限制條件，並為他命名
11. 在EMPLOYEE資料表新增一個外部鍵\(foreign key\)以確保員工不會被分派到一個不存在的部門。

{% tabs %}
{% tab title="1" %}
```text
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

## 作業練習－DDL-view\(p.208\)

1. 使用EMP資料表中員編、姓名、部門編號 建立一個EMP\_VU view，並將姓名欄改以EMPLOYEE
2. 顯示EMP\_VU view中的資料內容
3. 使用EMP\_VU view來顯示所有員工姓名及部門編號。
4. 新建一個名為DEPT20的view，包含部門20的所有員工編號、姓名、部門編號。將view資料項目命名為employee\_id, employee, department\_id，並設定不允許使用者透過DEPT20來更改員工所屬部門編號。
5. 顯示DEPT20 view欄位定義資料\(結構\)及其所有資料內容。
6. 試試看利用DEPT20 view將Smith轉調到部門30
7. 新建一個名為SALARY\_VU的view，包含所有員工姓名、部門名稱、薪資、薪資等級。 將view中的資料項目分別命名為employee,department,salary,grade 

{% tabs %}
{% tab title="1" %}
```text
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

