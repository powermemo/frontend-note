# DDL資料庫物件維護

## 視觀表



## 作業練習－DDL\(p.208\)

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

