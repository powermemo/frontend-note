---
description: 參照講義p.165 p.193
---

# DDL資料庫物件維護

## 新增物件



## 修改物件



## 刪除物件



## 視觀表



## 作業練習－DDL\(p.191\)

1. 用下列資料新建DEPARTMENT資料表  
   `column name	null?		data type`

   `id		NOT NULL	NUMERIC(7)`

   `name		NOT NULL	VARCHAR(24)`

2. 利用DEPT資料表，將資料新增至DEPARTMENT資料表中\(只新增相對的資料欄\)
3. 利用下列資料新建EMPLOYEE資料表  
   `column name	Null?		data Type`

   `id		NOT NULL	NUMERIC(7)`

   `last_name	NOT NULL	VARCHAR(24)`

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

