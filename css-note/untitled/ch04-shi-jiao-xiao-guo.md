---
description: p.165~p.202
---

# CH04 - 視覺效果

## 【15.單面陰影】

One-sided shadows p.165 \[[原網址](https://www.w3cplus.com/css3/css-secrets/one-sided-shadows.html)\]  
[codepen 15](https://codepen.io/ch-zhuchu/pen/ExgVKJK)

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1512/css-secrets-4-5.png)

## 【16.不規則的陰影】drop-shadow

Irregular drop shadows p.170 \[[原網址](https://www.w3cplus.com/css3/css-secrets/Irregular-drop-shadows.html)\]  
[codepen16](https://codepen.io/ch-zhuchu/pen/LYRpvxg) \| [filter-effect](https://www.w3.org/TR/filter-effects/) \| 

* ✅透明圖片
* ✅線性漸層做的透明折角
* ✅虛線（原點框線）
* ✅文字
* ❌clip-path

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1512/css-secrets-4-7.png)

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1512/css-secrets-4-8.png)

```css
/*filter: url(drop-shadow.svg#drop-shadow);*/
filter: drop-shadow(2px 2px 10px rgba(0,0,0,.5));
```

## 【17.色調】

Color tinting p.174 \[[原網址](https://www.w3cplus.com/css3/css-secrets/color-tinting.html)\]  \|  [codepen](https://codepen.io/ch-zhuchu/pen/zYKrOeY)17  
目標：全部圖片蓋上一層濾鏡，hover的時候才顯示全彩。

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1512/css-secrets-4-9.png)

{% tabs %}
{% tab title="sepia\(\)棕色" %}
飽和的橙黃色調，大多數像素的色相約為35-40。

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1512/css-secrets-4-10.png)
{% endtab %}

{% tab title="saturate\(\)澄黃色" %}
例如數值是hsl\(335, 100%, 50%\)

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1512/css-secrets-4-11.png)
{% endtab %}

{% tab title="混和" %}
![](https://www.w3cplus.com/sites/default/files/blogs/2015/1512/css-secrets-4-12.png)

```css
filter: sepia() saturate(4) hue-rotate(295deg);
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
`:hover`或`:focus`要回復原狀

```css
img {
    transition: .5s filter;
    filter: sepia() saturate(4) hue-rotate(295deg);
}
img:hover,
img:focus {
    filter: none;
}
```
{% endhint %}

## 【18.磨砂玻璃效果】

Frosted glass effectp.182\[[原網址](https://www.w3cplus.com/css3/css-secrets/frosted-glass-effect.html)\] \| [codepen18](https://codepen.io/ch-zhuchu/pen/MWjKYZQ)

AMOS的毛玻璃  \| 試做的[codepen](https://codepen.io/ch-zhuchu/pen/OJydGKb)

```css
backdrop-filter: blur(5px);
```

我不太喜歡書裡的做法，他是body和父元件都套用背景圖fixed，父元件再用::偽元素使用模糊

## 【19.折角效果】

Folded corner effectp.192\[[原網址](https://www.w3cplus.com/css3/css-secrets/folded-corner-effect.html)\]

數學題...我 PASS XD

