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
  font-size: $font-size;//⭐這邊使用
  max-width: 30px;
  margin: $margin;//⭐這邊使用
}
```
{% endtab %}
{% endtabs %}

## Nesting巢狀，對應html階層

```markup
<!--HTML的部分-->
<div class="wrap">
  <div class="item">
    <h2>i'm h2</h2>
    <div class="img"><img src="xxx.jpg"></div>
    <div class="txt">Lorem ipsum dolor sit amet.</div>
  </div>
</div>
```

```css
//SCSS的部分
$bg-color:lightblue;
.wrap{
  .item{
    width: 500px;
    background: lightblue;
    &:hover{//🟡偽元素
      background: darken($bg-color,15%);//🟡變暗
    }
    h2{
      font-size: 26px;
      color: tomato;
    }
    .img{
      border: 3px solid green;
      width: 200px;
    }
    .txt{
      font-size: 18px;
    }
  }
}
```

{% hint style="info" %}
* 使用偽元素時，以「&」開頭。
* darken是SASS的語法：`darken(變數名,數值);` 讓顏色變暗。
{% endhint %}

## @import導入

前面提到「.scss」儲存後，會自動轉寫一份「.map」還有「.css」檔。  
若只想要「導入」不希望「轉寫」的話，檔案命名就要以「\_」開頭，例如「\_var.scss」。  
如全域變數就可以放在裡面。

SCSS導入非常簡單，不用副檔名，直接輸入檔名即可。

```css
@import url(var);
//但實際測試後，好像不行用，要用下面的那個才行
@import "var";
```

## mixin

mixin就像JS的function  
用mixin的好處是，需要使用時才呼叫。

{% tabs %}
{% tab title="不帶參數" %}
~

```css
/*宣告*/
@mixin margin() {/*🟡宣告*/
    margin: 0 auto;
}

/*呼叫*/
@include margin();/*🟡呼叫*/
```
{% endtab %}

{% tab title="帶值" %}
~

```css
$null:null;
/*宣告*/
@mixin padding($num) {/*🟡參數放變數*/
    padding: $num auto;
}

/*呼叫*/
@include padding(5px);
/*或是不放值，可以用「null」*/
@include padding($null);
```
{% endtab %}

{% tab title="預設值" %}
.

```css
/*宣告*/
@mixin btn($w , $bgc , $fontSize:14px) {/*🟡「14px」是預設值*/
  width: $w;/*🔹*/
  padding: 10px;
  font-size: $fontSize;/*🔹*/
  text-align: center;
  border-radius: 30px;
  color: #fff;
  cursor: pointer;
  background-color: $bgc;/*🔹*/
  transition: .2s all ease-in;
  &:hover {
     background-color: darken($bgc , 10%);
  }
}

/*宣告*/
.item{
  .btn{
    @include btn(100px, tomato );/*🟡沒有帶第三個參數*/
  }
}
```
{% endtab %}
{% endtabs %}

## 字串轉數值

如class、路徑、屬性等都是字串需要做轉換

{% tabs %}
{% tab title="First Tab" %}
```markup
<div class="box"></div>
```

```css
/*以下是mixin的另一種用法「#{$var}」*/
@mixin test($var,$w,$bgc,$fz) {
    #{$var}{
        width: $w;
        background-color: $bgc;
        font-size: $fz;
        @content;/*「@content」的意思：若某些屬性不在(#{$var})裡面，可額外增加*/
    }
}
@include test('.box',150px,#f20,13px){/*有個div的class名稱為「box」*/
    border: 5px solid tomato;/*「#{var}」內沒有border的屬性，另外加上的。*/
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
* mixin的另一種用法「`#{$var}`」
  * 「`#{$var}`」內「`@content`」的意思：若某些屬性不在\(`#{$var}`\)裡面，可額外增加
  * `@include test('.box',150px,#f20,13px)`/\*有個div的class名稱為「box」\*/
{% endhint %}

## SASS運算 \| 運用

SASS可做運算

{% tabs %}
{% tab title="普通運算" %}
+-\*/

```css
$w:10;
$h:9;
.box{
    width: 10 + 10px;
    height: 10 - 5em;
    font-size: $w * $h + px;
    //斜線原本的意思：「font-sizt  /  line-hieght」
    //🟡所以除法一定要小括號框起來。    
    font: (15 / 5);
    color: #333 + #999;
}
```

```css
//CSS
.box {
  width: 20px;
  height: 5em;
  font-size: 90px;
  font: 3;
  color: #cccccc;
}
```
{% endtab %}

{% tab title="運算公式" %}
ex. floor, round

```css
//SCSS
.box2{
    //floor(x)不大於x的最大整數
    //ceil(x)不小於x的最小整數
    //round四捨五入
    width: floor(100px / 3);
    height: ceil(100px / 6);
    margin: round(100px / 8);
}
```

```css
//CSS
.box2{
    //floor(x)不大於x的最大整數
    //ceil(x)不小於x的最小整數
    //round四捨五入
    width: floor(100px / 3);
    height: ceil(100px / 6);
    margin: round(100px / 8);
}
```
{% endtab %}

{% tab title="字級" %}
h1~h3

```css
//SCSS
@import 'var';
/*這裡的「$font-size」是區域變數*/
@mixin titleH($font-size) {//宣告
    h1{font-size: round($font-size * 4.5);}
    h2{font-size: round($font-size * 3);}
    h3{font-size: round($font-size * 2.8);}
}
/*🟡這裡的「$font-size」是全域變數
  因為還是變數，他會去「@import 'var'」找這個變數*/
@include titleH($font-size);
```

```css
//CSS
h1 {font-size: 126px;}
h2 {font-size: 84px;}
h3 {font-size: 78px;}
```
{% endtab %}

{% tab title="條件" %}
if\_\_else

```css
//SCSS
@mixin bodyBgc($backgourndColor:black) {
    @if($backgroundColor == black and 
        $backgroundColor == #000){
        background-color: $backgroundColor;
    }
}
@mixin layout($width) {
    @if $width == 100{
        width: 100%;
        display: block;
    }@else{
        width: $width +px;
        margin: 0 auto;
    }
}

.wrap{
    @include layout(1366);
    @include bodyBgc(#333);
}
```

```css
//CSS
.wrap {
  width: 1366px;
  margin: 0 auto;
  background-color: black;
}
```
{% endtab %}

{% tab title="繼承" %}
@extend

若沒有要使用參數的話「@extend」會是比「@mixin」更好的用法～  
 [stackOverflow相似的說法](https://stackoverflow.com/questions/18008700/)

```css
//SCSS
//「%」佔位符號
//用「%」開頭就不會佔位了(不是一個class)
%rect{//🟡
    width: 100px;
    height: 50px;
}

%textAlign{//🟡
    text-align: center;
}

.green{
    background-color: green;
    @extend %rect;//🟡繼承屬性
    @extend %textAlign;
}
.red{
    background-color: red;
    @extend %rect;//🟡繼承屬性
    @extend %textAlign;
}
```

```css
//CSS
.green, .red {
  width: 100px;
  height: 50px;
}

.green, .red {
  text-align: center;
}

.green {
  background-color: green;
}

.red {
  background-color: red;
}
```
{% endtab %}

{% tab title="迴圈" %}
@for $i from 1 through 12{}

```css
//SCSS
@media all and (min-width:767px) and (max-width:1200px){
    @for $i from 1 through 12{
        .col-md-#{$i}{
            width:($i / 12) * 100%;
            display: block;
        }
    }
}

//grid-另一寫法
@mixin grids($key,$num){
    @for $i from 1 through $num{
        .con-#{$key}-#{$num}{
            width: ($i / $num) * 100%;
            @content;
        }
    }
}

@mixin grids($key,$num){
    @include grids(md, 12){
        display: block;
        text-align: center;
    }
}
```

```css
//CSS
@media all and (min-width: 767px) and (max-width: 1200px) {
  .col-md-1 {
    width: 8.33333%;
    display: block;
  }
  .col-md-2 {
    width: 16.66667%;
    display: block;
  }
  .col-md-3 {
    width: 25%;
    display: block;
  }
  .col-md-4 {
    width: 33.33333%;
    display: block;
  }
  .col-md-5 {
    width: 41.66667%;
    display: block;
  }
  .col-md-6 {
    width: 50%;
    display: block;
  }
  .col-md-7 {
    width: 58.33333%;
    display: block;
  }
  .col-md-8 {
    width: 66.66667%;
    display: block;
  }
  .col-md-9 {
    width: 75%;
    display: block;
  }
  .col-md-10 {
    width: 83.33333%;
    display: block;
  }
  .col-md-11 {
    width: 91.66667%;
    display: block;
  }
  .col-md-12 {
    width: 100%;
    display: block;
  }
}
```
{% endtab %}

{% tab title="grid" %}
格線系統

```css
//grid
@media all and (min-width:767px) and (max-width:1200px){
    @for $i from 1 through 12{
        .col-md-#{$i}{
            width:($i / 12) * 100%;
            display: block;
            background-color: green;
        }
    }
}

```

```css
// 編譯後看起來像這樣
@media all and (min-width: 767px) and (max-width: 1200px) {
  .col-md-1 {
    width: 8.33333%;
    display: block;
    background-color: green;
  }
  .col-md-2 {
    width: 16.66667%;
    display: block;
    background-color: green;
  }
  .col-md-3 {
    width: 25%;
    display: block;
    background-color: green;
  }
  .col-md-4 {
    width: 33.33333%;
    display: block;
    background-color: green;
  }
  .col-md-5 {
    width: 41.66667%;
    display: block;
    background-color: green;
  }
  .col-md-6 {
    width: 50%;
    display: block;
    background-color: green;
  }
  .col-md-7 {
    width: 58.33333%;
    display: block;
    background-color: green;
  }
  .col-md-8 {
    width: 66.66667%;
    display: block;
    background-color: green;
  }
  .col-md-9 {
    width: 75%;
    display: block;
    background-color: green;
  }
  .col-md-10 {
    width: 83.33333%;
    display: block;
    background-color: green;
  }
  .col-md-11 {
    width: 91.66667%;
    display: block;
    background-color: green;
  }
  .col-md-12 {
    width: 100%;
    display: block;
    background-color: green;
  }
}
```
{% endtab %}

{% tab title="each" %}
@each in

```css
//SCSS
$images: a1, a2, a3 box feature;//可給逗號、可不給
@each $img in $images{//🟡
    .#{$img}-img{
        background-image: url(./img/#{$img}.jpg);
        // @extend .bg-image;
    }
}
```

```css
//CSS
.a1-img {
  background-image: url(./img/a1.jpg);
}

.a2-img {
  background-image: url(./img/a2.jpg);
}

.a3-img {
  background-image: url(./img/a3.jpg);
}

.box-img {
  background-image: url(./img/box.jpg);
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
除法：

* 可以\(100px / 8\);
* 可以\(100 / 8\) + px;
* 不可以\(100 / 8px\);
{% endhint %}



