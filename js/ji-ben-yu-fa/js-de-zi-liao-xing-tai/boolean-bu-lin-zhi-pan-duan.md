# Boolean布林值，判斷

Boolean布林值只有兩個：true和false，判斷用。\
通常會搭配「if」「else」使用。

## 轉換為Boolean

{% tabs %}
{% tab title="Boolean()" %}
#### －`Boolean(`$$x$$`);` //這是一個函數

#### 數字

除了「0」和「NaN」其餘的數字都是true。\
範例：

`var a = -123;`\
`a = Boolean(a);`//a是布林、true

`var a = 0;`\
`a = Boolean(a);`//a是布林、**false**

#### 字串

除了「 」空字串，其他字串都是true。

#### 其他

「null」和「undefined」都是false。
{% endtab %}
{% endtabs %}



##
