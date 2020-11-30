# CH03－形狀

## 【01－靈活橢圓形】

Flexible ellipses\[[原網址](https://www.w3cplus.com/css3/css-secrets/flexible-ellipses.html)\]

{% tabs %}
{% tab title="橢圓形" %}
比較少人知道的方法，圓形可以調整水平與垂直的大小，用「/」隔開他們。  
`border-radius: 水平 / 垂直;`

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1510/css-secrets-4.png)

```css
border-radius: 100px / 75px;
```
{% endtab %}

{% tab title="半圓" %}
先說border-radius的組成：  
`border-radius: 10px / 5px 20px;` 等於 `border-radius: 10px 10px 10px 10px / 5px 20px 5px 20px;`  
\(左上.右上.右下.左下\)

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1510/css-secrets-6.png)

```css
border-radius: 50% / 100% 100% 0 0;
```

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1510/css-secrets-8.png)

```css
border-radius: 100% 0 0 100% / 50%;
```
{% endtab %}

{% tab title="1/4圓" %}
![](https://www.w3cplus.com/sites/default/files/blogs/2015/1510/css-secrets-9.png)

```css
border-radius: 100% 0 0 0;
```
{% endtab %}
{% endtabs %}

## 【02－平行四邊形】

Parallelograms\[[原網址](https://www.w3cplus.com/css3/css-secrets/parallelograms.html)\]  
`transform: skew();`  


{% tabs %}
{% tab title="問題" %}
直接放transform:skew\(\);  
文字也會變形。

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1510/css-secrets-14.png)
{% endtab %}

{% tab title="偽元素解決" %}
![](https://www.w3cplus.com/sites/default/files/blogs/2015/1510/css-secrets-15.png)

```css
.button {
    position: relative;
    /* text color, paddings, etc. */
}
.button::before {
    content: ''; /* To generate the box */
    position: absolute;
    top: 0; right: 0; bottom: 0; left: 0;
    z-index: -1;
    background: #58a;
    transform: skew(45deg);
}
```
{% endtab %}
{% endtabs %}

## 【03－菱形】

Diamond images\[[原網址](https://www.w3cplus.com/css3/css-secrets/diamond-images.html)\]

{% tabs %}
{% tab title="問題" %}
![](https://www.w3cplus.com/sites/default/files/blogs/2015/1510/css-secrets-19.png)
{% endtab %}

{% tab title="解決方案1" %}
![](https://www.w3cplus.com/sites/default/files/blogs/2015/1510/css-secrets-20.png)

```css
.picture {
    width: 400px;
    transform: rotate(45deg);
    overflow: hidden;
}
.picture > img {
    max-width: 100%;
    transform: rotate(-45deg) scale(1.42);
}
```

「scale\(1.42\)」是數學問題，不要問我。
{% endtab %}

{% tab title="解決方案2" %}
![](https://www.w3cplus.com/sites/default/files/blogs/2015/1510/css-secrets-22.png)

```css
img {
 clip-path: polygon(50% 0, 100% 50%,50% 100%, 0 50%);
 transition: 1s clip-path;
}
img:hover {
 clip-path: polygon(0 0, 100% 0,100% 100%, 0 100%);
}
```
{% endtab %}
{% endtabs %}

## 【04－斜切角】

Cutout corners\[[原網址](https://www.w3cplus.com/css3/css-secrets/cutout-corners.html)\]

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1510/css-secrets-23.png)

{% tabs %}
{% tab title="切角" %}
![](https://www.w3cplus.com/sites/default/files/blogs/2015/1510/css-secrets-29.png)

```css
/*CSS*/
background: #58a;
background:
 linear-gradient(135deg, transparent 15px, #58a 0)top left,
 linear-gradient(-135deg, transparent 15px, #655 0)top right,
 linear-gradient(-45deg, transparent 15px, #58a 0)bottom right,
 linear-gradient(45deg, transparent 15px, #655 0)bottom left;
background-size: 50% 50%;
background-repeat: no-repeat;
```

```css
/*SCSS*/
@mixin beveled-corners($bg, $tl:0, $tr:$tl, $br:$tl, $bl:$tr) {
background: $bg;
background:
 linear-gradient(135deg, transparent $tl, $bg 0) top left,
 linear-gradient(225deg, transparent $tr, $bg 0) top right,
 linear-gradient(-45deg, transparent $br, $bg 0) bottom right,
 linear-gradient(45deg, transparent $bl, $bg 0) bottom left;
background-size: 50% 50%;
background-repeat: no-repeat;
}

/*改參數的時候調整@mixin即可*/
@include beveled-corners(#58a, 15px, 5px);
```

```css
/*摻入SVG寫法*/
border: 20px solid transparent;
border-image: 1 url('data:image/svg+xml,\
 <svg xmlns="http://www.w3.org/2000/svg"\
 width="3" height="3" fill="%2358a">\
 <polygon points="0,1 1,0 2,0 3,1 3,2 2,3 1,3 0,2"/>\
 </svg>');
background: #58a;
background-clip: padding-box;
```

```css
/*clip-path*/
background: #58a;
clip-path: polygon(
 20px 0, calc(100% - 20px) 0, 100% 20px,
 100% calc(100% - 20px), calc(100% - 20px) 100%,
 20px 100%, 0 calc(100% - 20px), 0 20px
```
{% endtab %}

{% tab title="曲線切角" %}
![](https://www.w3cplus.com/sites/default/files/blogs/2015/1510/css-secrets-31.png)

```css
background: #58a;
background:
 radial-gradient(circle at top left, transparent 15px, #58a 0) top left,
 radial-gradient(circle at top right, transparent 15px, #58a 0) top right,
 radial-gradient(circle at bottom right, transparent 15px, #58a 0) bottom right,
 radial-gradient(circle at bottom left, transparent 15px, #58a 0) bottom left;
background-size: 50% 50%;
background-repeat: no-repeat;
```
{% endtab %}
{% endtabs %}

## 【05－梯形頁籤】

Trapezoid tabs\[[原網址](https://www.w3cplus.com/blog/1658.html)\]

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1510/css-secrets-39.png)

{% tabs %}
{% tab title="First Tab" %}
![&#x5B57;&#x6703;&#x504F;&#x4E0A;](https://www.w3cplus.com/sites/default/files/blogs/2015/1510/css-secrets-43.png)

```css
.tab {
    position: relative;
    display: inline-block;
    padding: .5em 1em .35em;
    color: white;
}
.tab::before {
    content: ''; /* To generate the box */
    position: absolute;
    top: 0; right: 0; bottom: 0; left: 0;
    z-index: -1;
    background: #58a;
    transform: perspective(.5em) rotateX(5deg);
}
```

![&#x89E3;&#x91CB;&#x70BA;&#x4EC0;&#x9EBC;&#x6703;&#x504F;&#x4E0A;](https://www.w3cplus.com/sites/default/files/blogs/2015/1510/css-secrets-45.png)

![transform-originbottom;](https://www.w3cplus.com/sites/default/files/blogs/2015/1510/css-secrets-45.png)

```css
transform: scaleY(1.3) perspective(.5em) rotateX(5deg);
transform-origin: bottom;
```

![&#x5FAE;&#x8ABF;&#x4E4B;&#x5F8C;](https://www.w3cplus.com/sites/default/files/blogs/2015/1510/css-secrets-47.png)
{% endtab %}

{% tab title="頁籤" %}
![](https://www.w3cplus.com/sites/default/files/blogs/2015/1510/css-secrets-48.png)

```css
nav > a {
 position: relative;
 display: inline-block;
 padding: .3em 1em 0;
}

nav > a::before {
 content: '';
 position: absolute;
 top: 0; right: 0; bottom: 0; left: 0;
 z-index: -1;
 background: #ccc;
 background-image: linear-gradient(
  hsla(0,0%,100%,.6),
  hsla(0,0%,100%,0));
 border: 1px solid rgba(0,0,0,.4);
 border-bottom: none;
 border-radius: .5em .5em 0 0;
 box-shadow: 0 .15em white inset;
 transform: perspective(.5em) rotateX(5deg);
 transform-origin: bottom;
}
```

把`transform-origin`的值改為`bottom left`或`bottom right`，我們就可以得到向左或向右傾斜的標籤。

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1510/css-secrets-49.png)
{% endtab %}
{% endtabs %}

## 【06－圓餅圖】

Simple pie charts p.150 \[[原網址](https://www.w3cplus.com/css3/designing-simple-pie-charts-with-css.html)\]

### CSS－做百分比

{% tabs %}
{% tab title="圓<50%" %}
[codepen](https://codepen.io/ch-zhuchu/pen/BaLNZQe)-14

![&#x4E00;&#x500B;&#x5712;&#xFF0C;&#x7528;&#x7DDA;&#x6027;&#x6F38;&#x5C64;&#x5206;&#x5169;&#x8272;](https://www.w3cplus.com/sites/default/files/blogs/2015/1508/pie-charts-2.png)

```markup
<div class="pie"></div>
```

```css
.pie {
  width: 100px; height: 100px;
  border-radius: 50%;
  background: yellowgreen;
  background-image: linear-gradient(to right, transparent 50%, #655 0);
}
```

![&#x7528;&#x507D;&#x5143;&#x7D20;::before&#x7576;&#x526A;&#x88C1;&#x906E;&#x8272;&#x7247;](https://www.w3cplus.com/sites/default/files/blogs/2015/1508/pie-charts-4.png)

```css
.pie::before {
  content: '';
  display: block;
  margin-left: 50%;
  height: 100%;
  border-radius: 0 100% 100% 0 / 50%;
  background-color: inherit; /*別用background*/
  transform-origin: left;
}
```

{% hint style="info" %}
 注意：不要使用`background: inherit;`，要用`background-color: inherit;`，  
否則父元素背景圖像上的漸變也會被繼承。
{% endhint %}

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1508/pie-charts-5.png)

分別展示不同百分比的餅圖，從左到右：10% \(36deg或.1turn\), 20% \(72deg或.2turn\), 40% \(144deg或.4turn\)

```css
.pie::before {
  content: '';
  display: block;
  margin-left: 50%;
  height: 100%;
  border-radius: 0 100% 100% 0 / 50%;
  background-color: inherit; /*別用background*/
  transform-origin: left;
  transform: rotate(.1turn);/*🟡*/
  /*10% (36deg或.1turn), 
    20% (72deg或.2turn), 
    40% (144deg或.4turn)*/
}
```
{% endtab %}

{% tab title="Second Tab" %}

{% endtab %}
{% endtabs %}



