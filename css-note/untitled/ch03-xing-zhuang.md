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

### CSS

[codepen14](https://codepen.io/ch-zhuchu/pen/BaLNZQe)

{% tabs %}
{% tab title="圓<50%" %}
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

{% tab title="園>50%" %}
問題：前一頁的圓形&gt;50%就會失效

![&#x4E0D;&#x662F;&#x6211;&#x5011;&#x8981;&#x7684;&#x7D50;&#x679C;](https://www.w3cplus.com/sites/default/files/blogs/2015/1508/pie-charts-6.png)

解決方法：只是將偽元素::before換個顏色。

```css
background: inherit;
```
{% endtab %}

{% tab title="delay做圓餅" %}
![](https://www.w3cplus.com/sites/default/files/blogs/2015/1508/pie-charts-8.png)

{% hint style="info" %}
 負延遲是有效的。和`0s`的延遲類似，它表示動畫將立即執行，但是是根據延遲的絕對值來自動運行的，所以如果動畫已經在指定的時間之前就開始運行了，那它就會直接從active的時間中途運行。— [CSS Animations Level 1](https://drafts.csswg.org/css-animations-1/#animation-delay)
{% endhint %}

動畫是永遠暫停的，我們給它指定的延遲大小並不會有什麼影響。

```markup
<div class="pie" style="animation-delay: -20s">20%</div> 
<div class="pie" style="animation-delay: -60s">60%</div>
```

```css
.pie {
  position: relative;
  width: 100px;
  line-height: 100px;
  border-radius: 50%;
  background: yellowgreen;
  background-image:
   linear-gradient(to right, transparent 50%, #655 0);
  color: transparent;
  text-align: center;
}
@keyframes spin {
  to { transform: rotate(.5turn); }
}
@keyframes bg {
  50% { background: #655; }
}
.pie::before {
  content: '';
  position: absolute;
  top: 0; left: 50%;
  width: 50%; height: 100%;
  border-radius: 0 100% 100% 0 / 50%;
  background-color: inherit;
  transform-origin: left;
  animation: spin 50s linear infinite,
   bg 100s step-end infinite;
  animation-play-state: paused;
  animation-delay: inherit;
}
```

```javascript
document.querySelectorAll('.pie').forEach(pie=>{
  let p = parseFloat(pie.textContent);
  pie.style.animationDelay = '-' + p + 's';
})
```
{% endtab %}

{% tab title="圓動畫" %}
帶動畫的：

```css
@keyframes bg {
  50% { background: #655; }
}
@keyframes spin {
  to { transform: rotate(.5turn); }
}
.pie::before {
  content: '';
  display: block;
  margin-left: 50%;
  height: 100%;
  border-radius: 0 100% 100% 0 / 50%;
  background-color: inherit;
  transform-origin: left;
  animation: spin 3s linear infinite,
             bg 6s step-end infinite;
}
```
{% endtab %}
{% endtabs %}

### SVG

SVG solution p.158  [codepen14-SVG](https://codepen.io/ch-zhuchu/pen/RwGPjbJ)

{% tabs %}
{% tab title="中空圓" %}
![SVG&#x756B;&#x4E00;&#x500B;&#x5713;&#xFF0C;&#x539A;&#x908A;&#x6846;](https://www.w3cplus.com/sites/default/files/blogs/2015/1508/pie-charts-9.png)

```markup
<svg width="100" height="100"> 
  <circle r="30" cx="50" cy="50" /> 
</svg>
```

```css
circle { 
  fill: yellowgreen; 
  stroke: #655; 
  stroke-width: 30; 
}
```

![&#x6709;&#x9593;&#x8DDD;&#x7684;&#x908A;&#x6846;](https://www.w3cplus.com/sites/default/files/blogs/2015/1508/pie-charts-10.png)

```css
stroke-dasharray: 20 10;
```

{% hint style="info" %}
`20`的長度+`10`的邊距  
 周長：`C = 2πr`,所以在這裡`C = 2π × 30 ≈ 189`
{% endhint %}

![0/189, 40/189, 95/189,150/189](https://www.w3cplus.com/sites/default/files/blogs/2015/1508/pie-charts-11.png)

```css
/*從左到右的虛線數值*/
stroke-dasharray: 0 189; 
stroke-dasharray: 40 189;
stroke-dasharray: 95 189;
stroke-dasharray: 150 189
```
{% endtab %}

{% tab title="實心圓" %}
![&#x7DDA;&#x7C97;&#x8DDF;&#x534A;&#x5F91;&#x4E00;&#x6A23;&#x5BEC;](https://www.w3cplus.com/sites/default/files/blogs/2015/1508/pie-charts-12.png)

```markup
<svg width="100" height="100" class="svg2">
  <circle r="25" cx="50" cy="50"  class="circle2"/>
</svg>
```

```css
.circle {
    fill: yellowgreen;
    stroke: #655;
    stroke-width: 50;
    stroke-dasharray: 60 158; /* 2π × 25 ≈ 158 */
}
```

![SVG&#x52A0;&#x4E0A;&#x4E00;&#x6A23;&#x7684;&#x88AB;&#x666F;&#x8272;&#x770B;&#x8D77;&#x4F86;&#x5C31;&#x662F;&#x4E00;&#x500B;&#x5927;&#x5713;](https://www.w3cplus.com/sites/default/files/blogs/2015/1508/pie-charts-13.png)

```css
.svg{
  transform: rotate(-90deg); 
  background: yellowgreen; /*你可以換色看看w*/
  border-radius: 50%;
}
```

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1508/pie-charts-14.png)

```markup


```
{% endtab %}

{% tab title="未來" %}
![](https://www.w3cplus.com/sites/default/files/blogs/2015/1508/pie-charts-13.png)

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1508/pie-charts-14.png)

```markup
<div class="pie pie1"></div>
<div class="pie pie2" data-value="64"></div>
<div class="pie pie3"></div>
```

```css
.pie {
  width: 100px; height: 100px;
  border-radius: 50%;
}
.pie1{
  background: conic-gradient(#655 20%, yellowgreen 0);
}
.pie2{
  background: conic-gradient(#655  attr(data-value %) , yellowgreen 0);
}/*目前attr(data-*)在偽元素content可以用*/
.pie3{
  background: conic-gradient(deeppink 20%,  #fb3 0,#fb3 30%, yellowgreen 0);
}
```

{% hint style="success" %}
`conic-gradient(#655 20%, yellowgreen 0);`  
跟線性漸層用法差不多。
{% endhint %}

{% hint style="danger" %}
目前`attr(data-*)`在偽元素content可以用
{% endhint %}
{% endtab %}
{% endtabs %}

