---
description: 全名：Regular Expression
---

# RegExp正規表示式

參考網站\[[link](https://www.fooish.com/javascript/regexp/)\]

**處理字串的方法**，Regex 用自己一套特殊的符號表示法，  
讓我們可以很方便的搜尋字串、取代字串、刪除字串或測試字串**是否符合樣式規則**。

## 基本概念

| Regex 表示式 | 說明 |
| :--- | :--- |
| \d{4}-\d{2}-\d{2} | 從文本裡找出 YYYY-MM-DD 格式的日期字串 |
| cat\|dog | 從文本裡找出 cat 或 dog 字串 |
| \[A-Z\]\w+ | 從文本裡找出所有字首是大寫的英文字 |
| ^\[A-Za-z\]\d{9}$ | 驗證字串是否是台灣身份證字號 |

## 基本語法

| 項目 | 符號 | 說明 | 範例 |
| :--- | :--- | :--- | :--- |
| 字元 |  | 單純照字面上的意義 | dog 可以用來匹配 dog 這字串 |
| 或 | \| | 將所有可能的選擇條件分隔開。 |  gray\|grey 可以用來匹配 gray 或是 grey 字串。 |
| 群組 | \(\) | 作用範圍或優先順序。 | gray\|grey 和 gr\(a\|e\)y 都同樣可以用來匹配 gray 或是 grey 字串。 |
| 量詞1 | ? | 連續出現 0 次或 1 次。 | colou?r 可以用來匹配 color 或 colour。 |
| 量詞2 | \* | 連續出現 0 次或多次。 | ab\*c 可以用來匹配 ac, abc, abbc, abbbc 或 abbbbbbc。 |
| 量詞3 | + | 連續出現 1 次或多次。 | ab+c 可以用來匹配 abc, abbc, abbbc, abbbbbbc，但 ac 不符合。 |
| 量詞4 | {min,max} | 至少連續出現 min 次， 但最多連續出現 max 次。 |  |

## 字元類別 \(Character Classes\)

{% tabs %}
{% tab title="." %}
. dot  
點號 \(dot or period\) . 用來匹配**除了換行符號** \(line breaks\) \n \r 之外的任何一個字元。

```javascript
/a.c/.test('abc');  // true
/a.c/.test('a#c');  // true
/a.c/.test('a\nc'); // false
```
{% endtab %}

{% tab title="\[ \]  \[^\]  \[-\]" %}
\[ \] character set  
\[ \] 中括號用來表示一個字元集合 \(character set\)，整個中括號代表一個字元，裡面的內容就是這個字元的所有可能。

* a\[abcde123\]c 可以用來匹配 "abc", "a1c" 等字串， 但不能匹配 "aGc", "a\_c", "a\#c", "a5c", "a c", "a\nc" 等字串。
* a\[\\]\]c 可以用來匹配 "a\]c" 字串。

```javascript
/a[abcde123]c/.test('abc'); // true
/a[abcde123]c/.test('a#c'); // false
/a[abcde123]c/.test('a_c'); // false
```

\[^ \] negated set  
\[^ \] 是 \[ \] 的相反，用來匹配不在字元集合裡面的字元。

* a\[^abcde123\]c 可以用來匹配 "aGc", "a\_c", "a\#c", "a5c", "a c", "a\nc" 等字串， 但不能匹配 "abc", "a1c" 等字串。

```javascript
/a[^abcde123]c/.test('abc'); // false
/a[^abcde123]c/.test('a#c'); // true
/a[^abcde123]c/.test('a_c'); // true
```

\[ \] \(或 \[^ \]\) 中還可以用 - 符號來表示連續 \(range\) 的好幾個字元。

* a\[a-zC-F3-7\]c 其中 a-z 表示 a 到 z 所有的小寫英文字、 C-F 表示大寫的 C 到 F \(C D E F\)、3-7 表示數字 3 到 7 \(3 4 5 6 7\)， 可以用來匹配 "abc", "a5c" 等字串，但不能匹配 "a1c", "aGc", "a\_c", "a\#c", "a c", "a\nc" 等字串。

```javascript
/a[a-zC-F3-7]c/.test('abc'); // true
/a[a-zC-F3-7]c/.test('a5c'); // true
/a[a-zC-F3-7]c/.test('aGc'); // false
```
{% endtab %}

{% tab title="\[\\s\\S\] " %}
\[\s\S\] match any  
\[\s\S\] 用來匹配任意一個字元，**包含換行符號**。

```javascript
/a[\s\S]c/.test('abc');  // true
/a[\s\S]c/.test('a#c');  // true
/a[\s\S]c/.test('a\nc'); // true
```
{% endtab %}

{% tab title="\\s \\S" %}
\s whitespace  
\s 用來匹配所有的空白字元 \(whitespace\) - 空白 \(space\)、tab 和換行符號 \r \n。

```javascript
/a\sc/.test('a c');  // true
/a\sc/.test('a5c');  // false
/a\sc/.test('a\nc'); // true
```

\S not whitespace  
\S 用來匹配 \s 以外的所有字。

```javascript
/a\Sc/.test('a c');  // false
/a\Sc/.test('a5c');  // true
/a\Sc/.test('a\nc'); // false
```
{% endtab %}

{% tab title="\\w \\W" %}
\w word  
\w 用來匹配所有大小寫英文字、阿拉伯數字和底線 \_。

{% hint style="info" %}
\w 意思同等於 \[A-Za-z0-9\_\]。
{% endhint %}

```javascript
/a\wc/.test('abc');  // true
/a\wc/.test('a#c');  // false
/a\wc/.test('a\nc'); // false
```

\W not word  
\W 用來匹配 \w 以外的所有字。

{% hint style="info" %}
 `\W` 意思同等於 `[^A-Za-z0-9_]`。
{% endhint %}

```javascript
/a\Wc/.test('abc');  // false
/a\Wc/.test('a#c');  // true
/a\Wc/.test('a\nc'); // true
```
{% endtab %}

{% tab title="\\d \\D " %}
\d digit  
\d 用來匹配所有阿拉伯數字 0-9。

{% hint style="info" %}
 `\d` 意思同等於 `[0-9]`。
{% endhint %}

```javascript
/a\dc/.test('abc');  // false
/a\dc/.test('a5c');  // true
/a\dc/.test('a\nc'); // false
```

\D not digit  
\D 用來匹配 \d 以外的所有字。

{% hint style="info" %}
 `\D` 意思同等於 `[^0-9]`。
{% endhint %}

```javascript
/a\Dc/.test('abc');  // true
/a\Dc/.test('a5c');  // false
/a\Dc/.test('a\nc'); // true
```
{% endtab %}
{% endtabs %}

## 錨點符號\(Anchors\)

{% tabs %}
{% tab title="^..." %}
^... beginning  
^ 用來表示只匹配以 ... 「開頭」的字串。

* ^hello 可以用來匹配 "hello world" 字串，但不能匹配 "say hello 123"
* 「多行」的字串中  
  `101`

  `hello Mike`  
   m 修飾詞 \(flag\) 讓 ^ 改成匹配「行首」， `/^hello/m` 即可用來匹配上面的字串。

```javascript
/^hello/.test('hello world');   // true
/^hello/.test('say hello 123'); // false
```
{% endtab %}

{% tab title="...$" %}
...$ end  
$ 用來表示只匹配以 ... 「結尾」的字串。

* foo$ 可以用來匹配 "bar foo" 字串，但不能匹配 "foo bar"。
* 在「多行」的字串中  
  `123 foo`

  `456`  
  加上 m 修飾詞 \(flag\) 讓 $ 改成匹配「行尾」， `/foo$/m` 即可用來匹配上面的字串。

```javascript
/foo$/.test('bar foo'); // true
/foo$/.test('foo bar'); // false
```
{% endtab %}

{% tab title="\\b  \\B" %}
\b word boundary  
\b 用來匹配單字邊界 \(word boundary\)，表示字元的「前面」或「後面」除了空白字元 \(whitespace\)、標點符號 \(punctuation\) 或是在字串開頭或結尾外不可再有其它字元。

* llo\b 可以用來匹配 "hello world", "hello\nworld", "hello", "hello, Mike"， 但不能用來匹配 "hello\_world", "helloworld", "hello101"。
* \bworld\b 可以用來匹配 "hello world", "hello~world", "world"， 但不能用來匹配 "helloworld", "01world"。

{% hint style="info" %}
 word boundary 可以看作是不屬於 [`\w`](https://www.fooish.com/regex-regular-expression/character-classes.html#w-word) 的字元。
{% endhint %}

```javascript
/llo\b/.test('hello world'); // true
/llo\b/.test('hello_world'); // false
```

\B not word boundary  
\B 則是相對於 \b，用來匹配非單字邊界 \(word boundary\)。

* llo\B 可以用來匹配 "hello\_world", "helloworld", "hello101"， 但不能用來匹配 "hello world", "hello\nworld", "hello", "hello, Mike"。
* \Bworld\B 可以用來匹配 "123worldxyz"， 但不能用來匹配 "helloworld", "hello world", "world"。

```javascript
/llo\B/.test('hello world'); // false
/llo\B/.test('hello_world'); // true
```
{% endtab %}
{% endtabs %}

## 修飾詞\(Flags\)

| flag | 意義 | 說明 |
| :--- | :--- | :--- |
| `i` | ignore case | 使用不區分大小寫的比對方式 |
| `m` | multiline | 使用多行模式，使 [`^`](https://www.fooish.com/regex-regular-expression/anchors.html#beginning) 和 [`$`](https://www.fooish.com/regex-regular-expression/anchors.html#end) 會比對每一行的開頭與結尾，而不是輸入字串的開頭和結尾 |
| `s` | singleline | 使用單行模式，使[句點 .](https://www.fooish.com/regex-regular-expression/character-classes.html#dot) 會比對每個字元，而不是換行符號 `\n` 以外的每個字元 |
| `g` | global search | 使用全局匹配模式。有時候你會希望重複匹配目標字串多次，使用 `g` flag 就可以保留 lastIndex 的狀態，讓下一次再匹配時，可以從 lastIndex 的位置開始找起，你就可以遍歷整個文本中的所有可匹配字串，而不是每一次再匹配時都得到一樣的結果 \(文本中從頭開始第一個找到的字串\)。另外預設上，如果沒有開啟 `g` flag，Regex 引擎只會返回「第一個」匹配到的字串結果 |

## 環顧Lookaround

 環顧Lookaround跟[錨點符號 \(anchor\)](https://www.fooish.com/regex-regular-expression/anchors.html) 有些類似，都用來做邊界檢查用的，不用來比對字元。

{% tabs %}
{% tab title="P\(?= \)" %}
**Positive Lookahead \(?= \)**  
語法 A\(?=B\)，括號中是想要檢視的內容，表示 A 後面必須是接著 B。

```php
// a 後面接的必須是 b, c 或 d 字元
/a(?=[bcd])/.test('ab');       //true
/a(?=[bcd])/.test('123acxyz'); //true
/a(?=[bcd])/.test('a101');     //false
/a(?=[bcd])/.test('ahi');      //false
```

```php
//找出 foo 且後面接的必須是 hello
/(?:foo)(?=hello)/.test('foohello');       //true
/(?:foo)(?=hello)/.test('this is foohello 123'); //true
/(?:foo)(?=hello)/.test('foohell');        //false
/(?:foo)(?=hello)/.test('123 foo hi');     //false
/(?:foo)(?=hello)/.test('oohello');        //false
```
{% endtab %}

{% tab title="N\(?! \)" %}
**Negative Lookahead** \(?! \)  
negative lookahead 是相對於 positive lookahead，只有在接下來的內容能不滿足指定條件的前提下，才會繼續進行匹配。

語法 A\(?!B\)，括號中是想要檢視的內容，表示 A 後面不能是接著 B。

```javascript
// a 後面接的不能是 b, c 或 d 字元
\a(?![bcd])\.text('a101');    　//true
\a(?![bcd])\.text('ahi');    　//true
\a(?![bcd])\.text('ab');    　//false
\a(?![bcd])\.text('123acxyz');//false
```

```javascript
//找出 foo 且後面接的不能是 hello
\(?:foo)(?!hello)\.text('foohell');        //true
\(?:foo)(?!hello)\.text('123 foo hi');        //true
\(?:foo)(?!hello)\.text('foohello');            //false
\(?:foo)(?!hello)\.text('this is foohello 123');//false
\(?:foo)(?!hello)\.text('oohello');            //false
```
{% endtab %}
{% endtabs %}

## 特殊字元

| 特殊字元 | 表示 | 說明 |
| :--- | :--- | :--- |
| `\000` | octal escape character | 000 是一個 2~3 位數的數字，表示 ASCII 字元的八進位代碼。例如 `\101` 表示大寫英文字元 A |
| `\xFF` | hexadecimal escaped character | FF 是兩位數的數字，表示 ASCII 字元的十六進位代碼。例如 `\x41` 表示大寫英文字元 A |
| `\uFFFF` | unicode escaped character | FFFF 是一個 4 位數的數字，表示 UTF-16 code unit |
| `\t` | tab character | tab 字元 |
| `\n` | line feed character | 換行字元 |
| `\v` | vertical tab character | vertical tab 字元 |
| `\f` | from feed character | from feed 字元 |
| `\r` | carriaage return character | carriaage return 字元 |
| `\0` | null character | null 字元 |
| `\.` | "." character | 點號字元 |
| `\\` | "" character | 反斜線字元 |
| `\+` | "+" character | 加號字元 |
| `\*` | "\*" character | 星號字元 |
| `\?` | "?" character | 問號字元 |
| `\^` | "^" character | ^ 字元 |
| `\$` | "$" character | 錢號字元 |
| `\[` | "\[" character | \[ 字元 |
| `\]` | "\]" character | \] 字元 |
| `\{` | "{" character | { 字元 |
| `\}` | "}" character | } 字元 |
| `\(` | "\(" character | \( 字元 |
| `\)` | "\)" character | \) 字元 |
| `\|` | "\|" character | 管線字元 |
| `\/` | "/" character | / 字元 |

## 範例

▼ Email Regex / Email 正規表示式

```javascript
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

▼ URL Regex / 網址正規表示式

```javascript
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
```

▼ IP Address Regex / IP 位址正規表示式

```javascript
/^(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$/
```

▼ HTML Tag Regex / HTML Tag 正規表示式

```javascript
/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/
```

## 🔸尋找匹配test\(\)、match\(\)

test\(\)方法和match\(\)方法式相反的格式。

```javascript
//語法
'string'.match(/regex/);
/regex/.test('string');

//test()
let extractStr = "Extract the word 'coding' from this string.";
let codingRegex = /coding/;
let result = codingRegex.test(extractStr);

//match()
let extractStr = "Extract the word 'coding' from this string.";
let codingRegex = /coding/;
let result = extractStr.match(codingRegex);
```

