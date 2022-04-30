---
description: 參照講義p.149~p.164
---

# DML資料庫維護&交易控制

## 新增表格內容-INSERT  INTO(p.150)

`INSERT INTO 表格名`\
`VALUES(欄1,欄2,...欄n);`

```
INSERT INTO emp[(指定欄位1,指定欄位2,...指定欄位n)]		(p.150)
VALUES(欄位1值,欄位2值,...欄位n值),
	    (欄位1值,欄位2值,...欄位n值),
	    (欄位1值,欄位2值,...欄位n值);
-- 🔹VALUES後每個小括號內都是 一筆 新增的資料，
-- 🔹可以新增多組(多筆)資料，用逗號「,」隔開。


INSERT INTO emp																		(p.158)
	SELECT *
	  FROM emp1
	  WHERE deptno=10;
-- 🔹emp1表單的資料新增(複製)到emp表單	
-- 🔹可以使用子查詢的方式新增（常用在備份）
```

## 修改表格內容-UPDATE  SET(p.152)

`UPDATE 表格名`\
`SET 修改欄位=修改值`\
`WHERE 條件判斷;`

{% tabs %}
{% tab title="範例" %}
```
-- 9-7將員編7782從部門10調到部門20    (p.152)
UPDATE emp
SET    deptno = 20
WHERE  empno = 7782;
```
{% endtab %}

{% tab title="範例2" %}
```
-- 9-8將員編7900的薪資改為1000    (p.152)
UPDATE emp
SET    sal = 1000
WHERE  empno = 7900;
```
{% endtab %}

{% tab title="更新兩欄資料" %}
```
-- 9-9將員編7369職稱改為salesman、部門改為30       (p.153)
UPDATE emp
SET    job = 'salesman',
       deoptno = 30
WHERE  empno = 7369;
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
關掉**安全機制`SET SQL_SAFE_UPDATES = 0 | 1;`**(0表關閉、1是預設值表開啟)\
PK、FK等原因，修改時會出問題。若設定安全機制關閉就可以修改了。
{% endhint %}

{% tabs %}
{% tab title="用子查詢取值" %}
```
-- 9-10員編7900在部門hr是哪個部門編號       (p.153)
-- 子查詢抓hr部門編號--70

UPDATE emp
SET deptno = (SELECT deptno
              FROM dept
              WHERE dname = 'hr') -- 70
WHERE empno = 7900;
```
{% endtab %}

{% tab title="用子查詢當條件用" %}
```
-- 將部門sales員工薪水+500       (p.153)
-- 子查詢抓部門sales的部門編號--30

UPDATE emp
SET sal = sal + 500
WHERE deptno = (SELECT deptno
                FROM dept
                WHERE dname = 'sales') -- 30
                
--示意圖
+-------+---------+---------+
| empno | sal     | sal+500 |
+-------+---------+---------+
|  7369 |  800.00 | 1300.00 |
|  7499 | 1600.00 | 2100.00 |
|  7521 | 1250.00 | 1750.00 |
|  7654 | 1250.00 | 1750.00 |
|  7698 | 2850.00 | 3350.00 |
|  7844 | 1500.00 | 2000.00 |
|  7900 |  950.00 | 1450.00 |
+-------+---------+---------+
7 rows in set (0.00 sec)
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
用子查詢合併使用時，兩者間資料表不可以是同一個。
{% endhint %}

## 刪除表格內容DELETE  FROM(p.154)

`DELETE FROM 表格名`\
`[WHERE 條件判斷];`

{% tabs %}
{% tab title="Plain Text" %}
```
-- 9-12從表格dept刪除部門70    (p.154)
DELETE FROM dept
WHERE deptno = 70;
```
{% endtab %}

{% tab title="子查詢條件" %}
```
-- 9-13刪除名稱有「public」的部門k              (p.155)
DELETE FROM emp
WHERE deptno = (SELECT deptno
              FROM dept
              WHERE dname LIKE '%public%');
```
{% endtab %}
{% endtabs %}



## 資料庫交易(p.159)

* COMMIT確認交易
* ROLLBACK放棄交易
* SAVEPOINT設定交易儲存點

![](<../.gitbook/assets/image (40).png>)

* 交易的一致性：交易影響多筆表單，要嘛都做，要嘛都不做，不可以做一半。&#x20;
* 不一致的舉例說明：訂單沒任何訂單項目、訂單成立但庫存沒減少

### 預設的交易控制(p.160)

自動確認`AUTOCOMMIT = 1` (每執行一次，就寫入硬碟執行)

### 起始一個交易(p.160)

* `SET AUTOCOMMIT = 0`&#x20;
* `BEGIN` | `START TRANSACTION`

### 結束一個交易(p.160)

* `SET AUTOCOMMIT = 1`
* `COMMIT`成立  /  `ROLLBACK`放棄

{% tabs %}
{% tab title="範例(p.162)" %}
```
START TRANSACTION;                        -- 設定交易區塊
    INSERT INTO tx VALUES (null,NOW());
ROLLBACK;                                 -- 取消交易(交易倒回)
```
{% endtab %}

{% tab title="範例2(p.162)" %}
```
SET AUTOCOMMIT = 0;                   -- 安全交易控制開始
    INSERT INTO tx VALUES(null,NOW());-- 交易開始
    ROLLBACK;                         -- 交易倒回
        /*可繼續其他交易進行*/

SET SUTOCOMMIT = 1;                   -- 安全交易控制結束
```
{% endtab %}
{% endtabs %}

### 交易控制(p.163)

![](<../.gitbook/assets/image (39).png>)

```
START TRANSACTION                    --(p.163)
    dml_statement;
    ...
    SAVEPOINT tx1;
    dml_statement;
    ...
    SAVEPOINT tx2;
    dml_statement;
    ...
    SAVEPOINT tx3;
    dml_statement;
    ...
    ROLLBACK TO tx3;  -- SAVEPOINT tx3
    ROLLBACK TO tx2;  -- SAVEPOINT tx2
    ROLLBACK TO tx1;  -- SAVEPOINT tx1
ROLLBACK;             -- undo
```

## 作業練習－DML(p.164)

1.  將下列資料新增至MY\_EMP資料表中，不列舉欄位

    `1	patel	Ralph	rpatel	795`
2.  使用列舉的方式將下列資料新增至my\_emp資料表中

    `2	dancs	betty	bdancs	860`
3.  將下列資料新增至my\_emp

    `3	biri	ben	bbiri	1100`

    `4	newman	chad	cnewman	750`
4. 將員工編號為3的名字(last name)更改為Drexler
5. 將薪資低於900元的所有員工調整為1000元
6. 確認資料更新已更改到資料庫中
7. 刪除Betty Dancs的資料
8.  /\*啟動一個資料庫交易

    &#x20;\* 將所有員工薪資調升10%

    &#x20;\* 設定一個交易儲存點

    &#x20;\* 刪除所有my\_emp資料庫中的資料

    &#x20;\* 確認資料已被你刪光了

    &#x20;\* 放棄刪除資料的動作

    &#x20;\* 確認交易\*/

{% tabs %}
{% tab title="1" %}
```
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
	SET last_name='Drexler' 
WHERE ID=3;

```
{% endtab %}

{% tab title="5" %}
```
-- 將薪資低於900元的所有員工調整為1000元

UPDATE my_emp 
	SET salary=1000 
WHERE salary<900;
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
