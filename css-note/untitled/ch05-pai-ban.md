---
description: p.204~p.252
---

# CH05－排版

## 【20連字】

Hyphenation p.204 \[[原網址](https://www.w3cplus.com/css3/css-secrets/hyphenation.html)\]

![](https://www.w3cplus.com/sites/default/files/blogs/2016/1601/css-secrets-5-2.png)

```css
hyphens: auto;
```

## 【21插入換行符】

Inserting line breaks p.208\[[原網址](https://www.w3cplus.com/css3/css-secrets/inserting-line-breaks.html)\]  
用偽元素`content: '\A';` 可以換行。

## 【22條斑馬條紋文本行】

Zebra-striped text lines p.214\[[原網址](https://www.w3cplus.com/css3/css-secrets/zebra-strlped-text-lines.html)\] \|[ codepen22](https://codepen.io/ch-zhuchu/pen/MWjKwxR)

![](https://www.w3cplus.com/sites/default/files/blogs/2016/1601/css-secrets-5-10.png)

先用一個淡色`background`，再用深色配透明線性漸層`background-img`組合。

```css
div{
  height: 150px;
  width: 180px;
  padding: .5em;
  line-height: 1.5;
  background: beige;
  background-size: auto 3em;
  background-origin: content-box;
  background-image: linear-gradient(rgba(0,0,0,.2) 50%,
                    transparent 0);
}
```

## 【23調整標籤寬度】

Adjusting tab width p.218 \[原網址\]

## 【24連體字母】

Ligatures p.220 \[[原網址](https://www.w3cplus.com/css3/css-secrets/ligatures.html)\]

```css
font-variant-ligatures: 
    common-ligatures 
    discretionary-ligatures 
    historical-ligatures;
```

好像沒用??

## 【25花式&】

Fancy ampersands p.224 \[[原網址](https://www.w3cplus.com/css3/css-secrets/fancy-ampersands.html)\]  
看起來只是換字體\(?\)  
 `<h1 class="amp">&amp;</h1>`

```css
@font-face {
  font-family: Ampersand;
  src: local('Baskerville-Italic'),
   local('GoudyOldStyleT-Italic'),
   local('Palatino-Italic'),
  local('BookAntiqua-Italic');
  unicode-range: U+26;
}
h1 {
  font-family: Ampersand, Helvetica, sans-serif;
}
```

## 【26自定義下底線】

Custom underlines p.230 \[[原網址](https://www.w3cplus.com/css3/css-secrets/custom-underlines.html)\]  
`text-decoration: underline;` ?

## 【27逼真的本文效果】

Realistic text effects p.236\[[原網址](https://www.w3cplus.com/css3/css-secrets/realistic-text-effects.html)\] \| [codepen27](https://codepen.io/ch-zhuchu/pen/dypMZxZ)

`text-shadow: x軸 y軸 模糊　顏色,其他組;`

`svg > text + use`  
CSS用stroke

## 【28環形文字】

Circular text p.246\[[原網址](https://www.w3cplus.com/css3/css-secrets/circular-text.html)\] \| [codepen28](https://codepen.io/ch-zhuchu/pen/qBaZpZV)  
SVG

![](https://www.w3cplus.com/sites/default/files/blogs/2016/1601/css-secrets-5-42.png)

{% tabs %}
{% tab title="HTML" %}
```markup
<div class="circular">
  <svg viewBox="0 0 100 100">
     <path d="M 0,50 a 50,50 0 1,1 0,1 z" id="circle" />
       <text><textPath xlink:href="#circle">
       circular reasoning works because
     </textPath></text>
  </svg>
</div>
```
{% endtab %}

{% tab title="CSS" %}
```css
.circular path { fill: none; }
.circular {
  width:  330px;
  height: 330px;
  margin: 3em auto 0;
}
.circular svg {
  display: block;
  overflow: visible;
  letter-spacing: 3px;
}
```
{% endtab %}
{% endtabs %}

