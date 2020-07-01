# JS命名

## 什麼時候需要命名？

常用的地方：

* 變數\(var\)
* 函數\(function\)
* 屬性名稱\(class\)
* ....等

## 命名的原則

* ✅ 可以使用**字母**大小寫、數字、錢字$及底線\_。
* 大小寫視為不同的名稱\(case-sensitive\)
* ❌ 不可以讓數字開頭。
* ❌ 不能用關鍵字\(以及未來保留字\) 例如 `var var = 3;` ~~JS：「你是在哈囉？」~~ 😒 ~~~~

### 關鍵字或保留字

以下是命名時不可以使用的單字。

|  |  |  |  |  |
| :--- | :--- | :--- | :--- | :--- |
| function | var | if | else | switch |
| for | case | do | return | with |
| in | break | delete | default | typeof |
| continue | finally | instanceof | throw | while |
| catch | this | void | new | try |
| false | true | null |  |  |

### 未來保留字

以下是命名時應該要避開的單字。

|  |  |  |  |  |
| :--- | :--- | :--- | :--- | :--- |
| abstract | double | implements | private | throws |
| boolean | enum | import | protected | transient |
| byte | export | int | public | volatile |
| char | extends | interface | short | class |
| final | long | static | const | float |
| native | super | debugger | goto  | package |
| synchronized |  |  |  |  |

## 語言命名的通則

大多數的程式語言皆是類似的命名方式。  
因為JS對於大小寫很敏感，所以命名要很小心警慎。

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x9805;<b>&#x76EE;</b>
      </th>
      <th style="text-align:left"><b>&#x547D;&#x540D;&#x65B9;&#x5F0F;</b>
      </th>
      <th style="text-align:left"><b>&#x8209;&#x4F8B;</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>&#x5167;&#x5EFA;&#x7269;&#x4EF6;</p>
        <p>(&#x8CC7;&#x6599;&#x578B;&#x614B;)</p>
      </td>
      <td style="text-align:left">
        <p>PascalCase</p>
        <p>&#x9996;&#x5B57;&#x5927;&#x5BEB;</p>
      </td>
      <td style="text-align:left">Number&#x3001;String&#x3001;RegExp</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x5C6C;&#x6027;/&#x65B9;&#x6CD5;</td>
      <td style="text-align:left">
        <p><b>camelCase</b>
        </p>
        <p><b>&#x99DD;&#x5CF0;&#x5F0F;&#x547D;&#x540D;</b>
        </p>
      </td>
      <td style="text-align:left">getElementById() //&#x9019;&#x662F;&#x65B9;&#x6CD5;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x81EA;&#x8A02;&#x6A19;&#x7C64;/&#x5C6C;&#x6027;/CSS</td>
      <td style="text-align:left">
        <p>kebab-case</p>
        <p>&#x70E4;&#x8089;&#x4E32;&#x547D;&#x540D;</p>
      </td>
      <td style="text-align:left">font-size</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x5E38;&#x6578;</td>
      <td style="text-align:left">&#x5168;&#x90E8;&#x5927;&#x5BEB;</td>
      <td style="text-align:left">Math.<b>PI</b>(&#x3C0;)</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x5E38;&#x6578;&#x8907;&#x5408;&#x5B57;</td>
      <td style="text-align:left">snake_case</td>
      <td style="text-align:left">MAX_VALUE</td>
    </tr>
    <tr>
      <td style="text-align:left">keyword/&#x4E8B;&#x4EF6;</td>
      <td style="text-align:left">&#x5168;&#x90E8;&#x5C0F;&#x5BEB;</td>
      <td style="text-align:left">var</td>
    </tr>
  </tbody>
</table>



