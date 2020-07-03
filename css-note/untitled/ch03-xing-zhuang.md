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
{% tab title="解決方案1" %}
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
{% endtab %}

{% tab title="Second Tab" %}

{% endtab %}
{% endtabs %}





