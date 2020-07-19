# SASS

## 安裝等前置作業

1. **安裝NODE.JS**  
   安裝長期穩定版\(LTS\) \[[官網連結](https://nodejs.org/en/)\]

   要查看安裝版本，打開命令提示字元\(CMD\)，輸入「`node -v`」

2. **安裝SASS** 在命令提示字元\(CMD\)輸入「`npm install -g sass`」 如果你用mac要輸入「`sudo npm install -g sass`」 更多詳情請見SASS\[[官網](https://sass-lang.com/install)\] 要查看安裝版本，命令提示字元\(CMD\)，輸入「`sass --version`」
3. VS code 安裝「**Live Sass Compiler**」  
   有像瀏覽器的console可以幫你查看哪裡有錯。  
   在vs code的JSON指令加上以下指令\(在「設定」尋找「SASS」按「Live Sass Compiler」\)

   ```text
   "liveSassCompile.settings.formats": [
           {
               "format": "expanded",
               "extensionName": ".css",
               "savePath": "/css/"
           }
       ],
   ```

## SASS簡介

SASS與SCSS的念法一樣，差在它們副檔名不同,還有...  
SASS的語法沒有「{}」和「;」，不可與CSS相容  
SCSS的語法有「{}」和「;」，可與CSS相容  
所以**一般會用SCSS**。

![](https://cdn-images-1.medium.com/max/1600/1*r7m8ZNvhIboyfsmlIdv9bw.png)

{% hint style="info" %}
更多介紹在SASS中文網 \[[連結](https://sass.bootcss.com/documentation)\]
{% endhint %}

## 變數型態

{% tabs %}
{% tab title="變數" %}
變數以「$」開頭命名\(有點像PHP\)

```css
$font-size : 20px;
$color : #333;
$margin : 10px 20px 30px 40px;  // list
$bg-color : (
  'blue' : #0059ff,
  'yellow' : #ffd900,
  'green' : #73ff00
); // map 數值 
$null : null;

body {
  $font-size : 210px;
  font-size: $font-size;
  max-width: 30px;
  margin: $margin;
}
```
{% endtab %}

{% tab title="Second Tab" %}

{% endtab %}
{% endtabs %}



