# JS命名

## 什麼時候需要命名？

常用的地方：

* 變數(var)
* 函數(function)
* 屬性名稱(class)
* ....等

## 命名的原則

* :white\_check\_mark: 可以使用**字母**大小寫、數字、錢字$及底線\_。
* 大小寫視為不同的名稱(case-sensitive)
* :x: 不可以讓數字開頭。
* :x: 不能用關鍵字(以及未來保留字)\
  例如 `var var = 3;` ~~JS：「你是在哈囉？」~~ :unamused: ~~~~&#x20;

### 關鍵字或保留字

以下是命名時不可以使用的單字。

|          |         |            |         |        |
| -------- | ------- | ---------- | ------- | ------ |
| function | var     | if         | else    | switch |
| for      | case    | do         | return  | with   |
| in       | break   | delete     | default | typeof |
| continue | finally | instanceof | throw   | while  |
| catch    | this    | void       | new     | try    |
| false    | true    | null       |         |        |

### 未來保留字

以下是命名時應該要避開的單字。

|              |         |            |           |           |
| ------------ | ------- | ---------- | --------- | --------- |
| abstract     | double  | implements | private   | throws    |
| boolean      | enum    | import     | protected | transient |
| byte         | export  | int        | public    | volatile  |
| char         | extends | interface  | short     | class     |
| final        | long    | static     | const     | float     |
| native       | super   | debugger   | goto      | package   |
| synchronized |         |            |           |           |

## 語言命名的通則

大多數的程式語言皆是類似的命名方式。\
因為JS對於大小寫很敏感，所以命名要很小心警慎。

| 項**目**                   | **命名方式**                                                       | **舉例**                  |
| ------------------------ | -------------------------------------------------------------- | ----------------------- |
| <p>內建物件</p><p>(資料型態)</p> | <p>PascalCase</p><p>首字大寫</p>                                   | Number、String、RegExp    |
| 屬性/方法                    | <p><strong>camelCase</strong></p><p><strong>駝峰式命名</strong></p> | getElementById() //這是方法 |
| 自訂標籤/屬性/CSS              | <p>kebab-case</p><p>烤肉串命名</p>                                  | font-size               |
| 常數                       | 全部大寫                                                           | Math.**PI**(π)          |
| 常數複合字                    | snake\_case                                                    | MAX\_VALUE              |
| keyword/事件               | 全部小寫                                                           | var                     |

