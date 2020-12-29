---
description: "基礎到不行\U0001F602。"
---

# 幼幼班

## JS寫在哪？

* 與HTML在**同一份檔案**內，記得要寫在開始結尾的標籤「&lt;script&gt;&lt;/script&gt;」

  * 可以寫在&lt;head&gt;&lt;/head&gt;標籤內。
  * 可以寫在&lt;body&gt;&lt;/body&gt;標籤內。
  * 可以同時存在&lt;head&gt;與&lt;body&gt;標籤內。

* 可以使用**外部連結**，HTML的檔案就用&lt;script&gt;標籤src連結。
  * 可以單獨寫在一個檔案內。
  * ES6語法，外部連結標籤可以加上`type="module"`，可以使用import和export功能

```markup
<script type="module" src="index.js"></script>
```

## JS的output輸出

三種JS常見的輸出方式：

* 「alert\(''\)」：彈出視窗
* 「document.write\(''\)」：新增在網頁段落（這個盡量不要用，會影響整個網頁）
* 「console.log\(''\)」：出現在瀏覽器開發者介面中

```javascript
<script>
    alert('彈出警告視窗!')//出現警告視窗「彈出警告視窗!」
    document.write('網頁段落')//出現在網頁中，有個段落「網頁段落」
    console.log('開發者介面裡')//出現在瀏覽器「開發者介面」的「console」
</script>
```

## JS怎麼註解？

~~不要問，你會怕。~~  
跟CSS一樣，/\*\*/多行註解。//單行註解

```javascript
//單行註解
/* 多行
      註解。
*/
```

## JS的眉角

* 嚴格區分大小寫。 alert\(\)正確；Alert\(\)不正確。
* 每一條code要用分號「;」結尾\(新版例如ES6比較不介意，但PHP會很介意\)。
* 自動忽略多餘的空格及換行。

## JS的定數與變數

* 定數，例如1 2 3 4 5 6 7 ...。
* 變數，例如 `var nmsl = 7788;`，「`nmsl`」就是一個變數。

