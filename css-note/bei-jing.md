# 背景

## 多重背景

先打的圖片會在前面\[[w3c](https://www.w3schools.com/css/tryit.asp?filename=trycss3_background_multiple)\]

{% tabs %}
{% tab title="HTML" %}
```markup
<div id="example1">
  <h1>Lorem Ipsum Dolor</h1>
  <p>Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat.</p>
  <p>Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.</p>
</div>
```
{% endtab %}

{% tab title="CSS" %}
```css
#example1 {
  background-image: url(img_flwr.gif), url(paper.gif);
  background-position: right bottom, left top;
  background-repeat: no-repeat, repeat;
  padding: 15px;
}
```
{% endtab %}
{% endtabs %}



## 希望可以有透明的body身體背景

訣竅

* 利用**::after偽元素**增加背景圖片，並設定透明度。
* body設定「relative」； body::after設定「**absolute**」、還有「**top/bottom/left/right:0**」
* body::after要加「**z-index\(負值\)**」才不會蓋到網頁上其他的東西哦～

{% tabs %}
{% tab title="CSS" %}
```css
body{/*本體的透明背景(在最下面)*/
  position: relative;
  background: linear-gradient( #a9f,#9ff)
    fixed center center / 100% 100%;
}

body::after{ /*重複透明的圖片蓋在body上*/
  position:absolute;
   content:'';
   background: url(https://picsum.photos/100/100/?random=4);
   opacity:.2;
   top: 0; 
   bottom: 0; 
   right: 0; 
   left: 0; 
   z-index: -1; 
}
```
{% endtab %}
{% endtabs %}

## 漸層背景對可視範圍作用

我不要整個網頁底部才看得到我的另一色，我想要「vh」+「fixed」的效果。

![&#x5927;&#x6982;&#x662F;&#x9019;&#x6A23;&#x7684;&#x611F;&#x89BA;](../.gitbook/assets/image%20%2828%29.png)

background設定「linear-gradient」按下**空白鍵**後繼續加上其他屬性  
「**fixed**」「**center center / 100% 100%**」

{% tabs %}
{% tab title="CSS" %}
```css
background: linear-gradient( #a9f,#9ff)
    fixed center center / 100% 100%;
```
{% endtab %}
{% endtabs %}

## 奇特的padding-top:100%背景\[[link](https://codepen.io/ch-zhuchu/pen/qBOwJGW)\]

![](../.gitbook/assets/image%20%2826%29.png)

{% tabs %}
{% tab title="HTML" %}
```markup
<main class="main">
  <ul class="img_list">
    <li><div class="img_block -a"></div></li>
    <li><div class="img_block -b"></div></li>
    <li><div class="img_block -c"></div></li>
    <li><div class="img_block -d"></div></li>
  </ul>
</main>
```
{% endtab %}

{% tab title="CSS" %}
```css
main.main ul.img_list > li{
  display: inline-block;
  list-style: none;
  width: 25%;
}
div.img_block{
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
  height: 20rem;
}
@media screen and (max-width:767px) {
  main.main ul.img_list li{
    width: 50%;
  }
}
```
{% endtab %}
{% endtabs %}

## 圖片框\[[link](https://www.webmart.tw/blog/45-css-border-and-box-effect/)\]

## 

## 自設透明圖片\(遮罩\)

{% embed url="https://bennettfeely.com/clippy/" %}

舉例（六角形）：

![](../.gitbook/assets/image%20%2832%29.png)

```css
clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
```

