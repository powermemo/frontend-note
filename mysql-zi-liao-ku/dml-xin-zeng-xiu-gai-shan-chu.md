# DML資料庫維護&交易控制

## 新增表格內容

`INSERT INTO 表格名  
VALUES(欄1,欄2,...欄n);`

```text
INSERT INTO emp[(指定欄位1,指定欄位2,...指定欄位n)]
VALUES(欄位1值,欄位2值,...欄位n值),
	(欄位1值,欄位2值,...欄位n值),
	(欄位1值,欄位2值,...欄位n值);
-- 🔹VALUES後每個小括號內都是 一筆 新增的資料，
-- 🔹可以新增多組(多筆)資料，用逗號「,」隔開。


INSERT INTO emp
	SELECT *
	  FROM emp1
	  WHERE deptno=10;
-- 🔹emp1表單的資料新增(複製)到emp表單	
-- 🔹可以使用子查詢的方式新增（常用在備份）
```

## 修改表格內容

`UPDATE 表格名  
SET 修改欄位=修改值  
WHERE 條件判斷;`



## 刪除表格內容

`DELETE FROM 表格名  
[WHERE 條件判斷];`



## 資料庫交易



## 作業練習－DML\(p.164\)

1. 將下列資料新增至MY\_EMP資料表中，不列舉欄位

   `1	patel	Ralph	rpatel	795`

2. 使用列舉的方式將下列資料新增至my\_emp資料表中

   `2	dancs	betty	bdancs	860`

3. 將下列資料新增至my\_emp

   `3	biri	ben	bbiri	1100`

   `4	newman	chad	cnewman	750`

4. 將員工編號為3的名字\(last name\)更改為Drexler
5. 將薪資低於900元的所有員工調整為1000元
6. 確認資料更新已更改到資料庫中
7. 刪除Betty Dancs的資料
8. /\*啟動一個資料庫交易

    \* 將所有員工薪資調升10%

    \* 設定一個交易儲存點

    \* 刪除所有my\_emp資料庫中的資料

    \* 確認資料已被你刪光了

    \* 放棄刪除資料的動作

    \* 確認交易\*/

{% tabs %}
{% tab title="1" %}
```text
/*將下列資料新增至MY_EMP資料表中，不列舉欄位
1	patel	Ralph	rpatel	795*/

INSERT INTO my_emp 
	VALUES(1,'Patel','Ralph','rpatel',795);
	
Query OK, 1 row affected (0.10 sec)
```
{% endtab %}

{% tab title="2" %}
```
/*使用列舉的方式將下列資料新增至my_emp資料表中
2	dancs	betty	bdancs	860*/

INSERT INTO my_emp(id,last_name, first_name, userid, salary) 
	VALUES(2,'Dances','Betty','bdances',860);
```
{% endtab %}

{% tab title="3" %}
```
/*將下列資料新增至my_emp
3	biri	ben	bbiri	1100
4	newman	chad	cnewman	750*/

INSERT INTO my_emp 
	VALUES(3,'Biri','Ben','bbiri',1100),
		  (4,'Newman','Chad','cnewmam',750);
```
{% endtab %}

{% tab title="4" %}
```
-- 將員工編號為3的名字(last name)更改為Drexler

SET SQL_SAFE_UPDATES = 0;
UPDATE my_emp 
	SET last_name='Drexler' WHERE ID=3;

```
{% endtab %}

{% tab title="5" %}
```
-- 將薪資低於900元的所有員工調整為1000元

UPDATE my_emp 
	SET salary=1000 WHERE salary<900;
```
{% endtab %}

{% tab title="6" %}
```
-- 確認資料更新已更改到資料庫中



```
{% endtab %}

{% tab title="7" %}
```
-- 刪除Betty Dancs的資料

DELETE FROM my_emp 
	WHERE userid='bdances';
```
{% endtab %}

{% tab title="8" %}
```
/*啟動一個資料庫交易
 * 將所有員工薪資調升10%
 * 設定一個交易儲存點
 * 刪除所有my_emp資料庫中的資料
 * 確認資料已被你刪光了
 * 放棄刪除資料的動作
 * 確認交易*/
 
 
 START TRANSACTION;
  UPDATE my_emp SET salary = salary * 1.1;
  SAVEPOINT SP1;
  DELETE FROM my_emp;
  SELECT COUNT(*) FROM my_emp;
  ROLLBACK TO SP1;
  COMMIT;
```
{% endtab %}
{% endtabs %}

