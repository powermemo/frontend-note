# 表格table

## 表格倒圓角\[[link](https://pjchender.blogspot.com/2015/12/table-with-border-radius.html)\]

{% tabs %}
{% tab title="原本的鳥樣" %}
![](https://4.bp.blogspot.com/-l6XNJFt6_MA/Vm_Wu_ObrWI/AAAAAAAAc_c/BSsTfqvRuKA/s1600/%25E8%259E%25A2%25E5%25B9%2595%25E6%2593%25B7%25E5%258F%2596%25E7%2595%25AB%25E9%259D%25A2_121515_050057_PM.jpg)

```css
table{
  border-collapse: collapse;
}
tr{
  border: 1px solid #E0607E;
}
td{
  border-radius: 10px;
  border: 1px solid #607ee0;
  padding: 10px 30px;
  background-color: #E0607E;
  color: #FFF;
}
```
{% endtab %}

{% tab title="separate" %}
![](https://3.bp.blogspot.com/-T8JrcAEF3xQ/VnAGB02tXMI/AAAAAAAAdAc/NdQUIIGkrrU/s400/2015-12-15_20-21-15.png)

```css
table{
  border-collapse: separate;
}
```
{% endtab %}

{% tab title="+spacing" %}
![](https://1.bp.blogspot.com/-ooeumMOIl2A/VnAHUG060bI/AAAAAAAAdAw/yXvdkUSaSFg/s1600/2015-12-15_20-27-15.png)

```css
table{
  border-collapse: separate;
  border-spacing: 0;
}
```
{% endtab %}

{% tab title="只有頭尾" %}
![](https://1.bp.blogspot.com/-q0H303e-okI/VnAJT3ojSPI/AAAAAAAAdBA/JKweSzIY4QY/s1600/2015-12-15_20-35-30.png)

```css
td:first-child{
  border-top-left-radius: 10px;
  border-bottom-left-radius: 10px;
}

td:last-child{
  border-top-right-radius: 10px;
  border-bottom-right-radius: 10px;
}
```
{% endtab %}

{% tab title="多欗多列" %}
{% embed url="https://codepen.io/PJCHENder/pen/obbXVr" %}

```css
/*第一欄第一列：左上*/
tr:first-child td:first-child{
  border-top-left-radius: 10px;
}
/*第一欄最後列：左下*/
tr:last-child td:first-child{
  border-bottom-left-radius: 10px;
}
/*最後欄第一列：右上*/
tr:first-child td:last-child{
  border-top-right-radius: 10px;
}
/*最後欄第一列：右下*/
tr:last-child td:last-child{
  border-bottom-right-radius: 10px;
}
```
{% endtab %}
{% endtabs %}

