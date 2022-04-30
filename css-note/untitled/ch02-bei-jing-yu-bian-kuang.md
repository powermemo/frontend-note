# CH02－背景與邊框

## 【01－透明邊框】

是在說「background-clip」\[[原網址](https://www.w3cplus.com/css3/css-secrets/translucent-borders.html)]\
原本內容會包含邊框範圍，「background-clip: padding-box;」可以讓邊框在內容外。

{% tabs %}
{% tab title="使用前" %}
![邊框設透明度，染到背景色。](<../../.gitbook/assets/image (2).png>)

```css
.txt{
  border: 10px solid rgba(50,150,0,.5);
  background-color: tomato;
}
```
{% endtab %}

{% tab title="使用後" %}
![](<../../.gitbook/assets/image (30).png>)

```css
.txt{
  border: 10px solid rgba(50,150,0,.5);
  background-color: tomato;
  background-clip: padding-box;
}
```

background-clip的其他選項：

![background-clip:;的其他選項](<../../.gitbook/assets/image (35).png>)
{% endtab %}
{% endtabs %}

## 【02－多重邊框】

border無法設多重邊框。\
解套方案\[[原網址](https://www.w3cplus.com/css3/css-secrets/multiple-borders.html)]

{% tabs %}
{% tab title="box-shadow" %}
### ■ box-shadow

用逗號「,」區分組，

* 第一個陰影會在最上層。
* 越外面的陰影，設定的寬度會越寬。
* 這些陰影並不會增加內容空間（你要自己調）。

```css
background: yellowgreen;
box-shadow: 0 0 0 10px #655, 0 0 0 15px deeppink;
```

![](<../../.gitbook/assets/image (13).png>)
{% endtab %}

{% tab title="outline" %}
### ■ outline

![](<../../.gitbook/assets/image (36).png>)

```css
  background: yellowgreen;
  border: 10px solid #655;
  outline: 15px solid deeppink;
```

限制：

* 只能畫到第二層
* 不能設定圓角

![](<../../.gitbook/assets/image (9).png>)
{% endtab %}
{% endtabs %}



## 【03－活用背景定位】

\[[原網址](https://www.w3cplus.com/css3/spheres.html)]

![不美觀的背景位置](<../../.gitbook/assets/image (27).png>)

{% tabs %}
{% tab title="background-position" %}
### ■ 增強型background-position:bottom right;

用偏移的方式移動。

![不同邊指定偏移量，如圖虛線所示。](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-2-11.png)

```css
background: url(code-pirate.svg) no-repeat #58a
                 bottom right;//這個部分是給不支援background-position瀏覽器
background-position: right 20px bottom 10px;
```
{% endtab %}

{% tab title="background-origin" %}
### ■ background-origin: content-box;

為的使程式碼更簡潔

```css
padding: 10px;
background: url(code-pirate.svg) no-repeat #58a;
background-position: right 10px bottom 10px;
```

其他選項

* border-box
* content-box&#x20;
* inherit&#x20;
* initial&#x20;
* padding-box&#x20;
* unset
{% endtab %}

{% tab title="calc()" %}
### ■ calc計算機

```css
background: url("code-pirate.svg") no-repeat;
background-position: calc(100% - 20px) calc(100% - 10px);
```

{% hint style="info" %}
記得calc的減號「-」前後都要加空白鍵哦！一定要加哦！！
{% endhint %}
{% endtab %}
{% endtabs %}



## 【04－內凹圓角】

外面矩形、裡面圓角怎麼做？\[[原網址](https://www.w3cplus.com/css3/css-secrets/inner-rounding.html)]

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-2-15.png)

{% tabs %}
{% tab title="1st" %}
第一種寫法，使用兩個div。

HTML的部分：

```markup
<div class="something-meaningful"><div>
 I have a nice subtle inner rounding,
 don’t I look pretty?
</div></div>
```

CSS的部分：

```css
.something-meaningful {
background: #655;
padding: .8em;
}
.something-meaningful > div {
background: tan;
border-radius: .8em;
padding: 1em;
}
```
{% endtab %}

{% tab title="2nd" %}
利用「background」的特性。

* 先將內容設定圓角。
* 使用「box-shadow」增加圓角外框。
* 使用「outline」增加最外層尖角外框。

```css
background: tan;
border-radius: .8em;
padding: 1em;
box-shadow: 0 0 0 .6em #655;
outline: .6em solid #655;
```

不能使用「border」，因為「outline」沒辦法覆蓋「border」。它們之間會產生空隙。

![你看，產生空隙了！](<../../.gitbook/assets/image (22).png>)
{% endtab %}

{% tab title="2nd的解釋" %}
馬的數學題🙃

![高中的三角形勾股定理。](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-2-19.png)

Q.三角形怎麼算斜角？ A.直角的兩邊平方和開根號。

最小的面積寬度：$$r√2-r = r(√2-1)$$ \
&#x20;$$r$$ = border-radius: .8em;\
&#x20;$$8(√2-1) ≈$$ .33137085em $$≈$$  .34em

$$(√2-1)<0.5$$ \
陰影半徑要  > $$(√2-1)r$$ \
陰影半徑要  <  outline寬度，\
也就是說outline寬度至少要 > $$(√2-1)r$$ 。
{% endtab %}
{% endtabs %}



## 【05－條紋背景】（漸層）

使用「linear-gradient」線性漸層製作。\[[原網址](https://www.w3cplus.com/css3/css-secrets/striped-backgrounds.html)]\
變化型漸層使用「repeating-linear-gradient」。

![我想要條紋背景怎麼弄？](<../../.gitbook/assets/image (31).png>)

{% tabs %}
{% tab title="普通漸層" %}
![](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-20.png)

```css
background: linear-gradient(#fb3, #58a);
```
{% endtab %}

{% tab title="兩色分明" %}
使兩色的過渡點在同個位置（在「linear-gradient」顏色後加上過渡點位置）。\
黃色的漸層（0%\~50%），藍色的漸層（50%\~100%）。\
這裡的百分比是指位置。

![兩色過渡點都在50%（正中間）](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-23.png)

```css
background: linear-gradient(#fb3 50%, #58a 50%);
```
{% endtab %}

{% tab title="調整大小" %}
加入「background-size」調整線性漸層大小。\
background-size: 寬度 高度;

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-25.png)

```css
background: linear-gradient(#fb3 50%, #58a 50%);
background-size: 100% 30px;
```
{% endtab %}

{% tab title="不等寬" %}
秘訣就是，條整兩色過渡點的位置。

黃色的過渡點30px高（0%\~30%）、藍色過渡點30px高（30%～100%）。\
**那個藍色的「0」寫法有點特別，注意一下哦～**

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-26.png)

```css
background: linear-gradient(#fb3 30%, #58a 0);
background-size: 100% 30px;
```
{% endtab %}

{% tab title="三色" %}
很簡單，只要再加入一色即可。

藍色的部分「#58a 0,」表示從上一色的尾部開始（就是黃色33.3%）；\
　　　　　「#58a 66.6%」表示尾部的位置到66.6%。

綠色的部分「yellowgreen 0」它沒有特地寫自己尾部最後到哪裡，\
表示從上一色尾部開始（就是藍色66.6%）一直到最後100%。

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-27.png)

```css
background: linear-gradient(
                #fb3 33.3%,
                #58a 0, #58a 66.6%, 
                yellowgreen 0);
background-size: 100% 45px;
```
{% endtab %}

{% tab title="垂直" %}
改變漸層方向「to right」或是直接給度數「90deg」也可。

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-28.png)

```css
background: linear-gradient(to right, /* or 90deg */
 #fb3 50%, #58a 0);
background-size: 30px 100%;
```
{% endtab %}

{% tab title="45°" %}
進階一點囉！

![怎麼弄？求助🙏](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-31.png)

![如果只有條45deg，就會變成這樣。](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-29.png)

```css
//這是上方方格的寫法
background: linear-gradient(45deg,
                #fb3 50%, #58a 0);
background-size: 30px 30px;
```

![這樣比較清楚了嗎？知道怎麼調了吧！（你在嗆什麼](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-30.png)

```css
background: linear-gradient(45deg,
                #fb3 25%, #58a 0, #58a 50%,
                 #fb3 0, #fb3 75%, #58a 0);
background-size: 30px 30px;
```

關於為什麼斜條紋的寬度比水平垂直的條紋還窄，請去看原網址～\
我不想再貼數學的咚咚了w🤪

另一個「**repeating-linear-gradient**」的寫法：

```css
background: repeating-linear-gradient(45deg,
                #fb3, #fb3 15px, 
                #58a 0, #58a 30px);
```
{% endtab %}

{% tab title="變化條紋" %}
## 「**repeating-linear-gradient**」無限重複。

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-35.png)

```css
background: repeating-linear-gradient(45deg,
 #fb3, #58a 30px);
```

以下code等同於上方code

```css
background: linear-gradient(45deg,
 #fb3, #58a 30px,
 #fb3 30px, #58a 60px,
 #fb3 60px, #58a 90px,
 #fb3 90px, #58a 120px,
 #fb3 120px, #58a 150px, ...);
```
{% endtab %}

{% tab title="60°" %}
## 「**repeating-linear-gradient**」

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-36.png)

```css
background: repeating-linear-gradient(60deg,
                #fb3, #fb3 15px, 
                #58a 0, #58a 30px);
```
{% endtab %}
{% endtabs %}

{% hint style="success" %}
可以看原網址出來的 [CodePen](https://codepen.io/ch-zhuchu/pen/QWKybXJ)
{% endhint %}

## 【06－複雜背景圖案】

使用**Sass**減少CSS重複背景的動作。\[[原網址](https://www.w3cplus.com/css3/css-secrets/complex-background-pattern.html)]\
你知道嗎，我根本還沒學Sass，我打算都用貼的🤪...

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-38.png)

{% tabs %}
{% tab title="懷舊方格" %}
感謝老天，這裡是用CSS

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-39.png)

```css
background: white;
background-image: linear-gradient(90deg,
                rgba(200,0,0,.5) 50%, transparent 0),/*直的*/
                 linear-gradient(
                rgba(200,0,0,.5) 50%, transparent 0);/*橫的*/
background-size: 30px 30px;
```
{% endtab %}

{% tab title="網格" %}
把過渡點變窄後～

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-40.png)

```css
background: #58a;
background-image:
 linear-gradient(white 1px, transparent 0),
 linear-gradient(90deg, white 1px, transparent 0);
background-size: 30px 30px;
```

進階的網格

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-41.png)

```css
background: #58a;
background-image:
 linear-gradient(white 2px, transparent 0),
 linear-gradient(90deg, white 2px, transparent 0),
 linear-gradient(hsla(0,0%,100%,.3) 1px,
 transparent 0),
 linear-gradient(90deg, hsla(0,0%,100%,.3) 1px,
 transparent 0);
background-size: 75px 75px, 75px 75px,
 15px 15px, 15px 15px;
```
{% endtab %}

{% tab title="波爾卡圓點" %}
![](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-43.png)

```css
background: #655;
background-image: radial-gradient(tan 30%, transparent 0),
 radial-gradient(tan 30%, transparent 0);
background-size: 30px 30px;
background-position: 0 0, 15px 15px;
```



下面的東西我不確定它是什麼，我想相信它是Sass

```css
@mixin polka($size, $dot, $base, $accent) {
background: $base;
background-image:
 radial-gradient($accent $dot, transparent 0),
 radial-gradient($accent $dot, transparent 0);
background-size: $size $size;
background-position: 0 0, $size/2 $size/2;
}
```

當要件例「polka」圓點的時候，再加入下面一行

```css
@include polka(30px, 30%, #655, tan);
```
{% endtab %}

{% tab title="棋盤格" %}
![](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-44.png)

先來一部不了解它怎麼產生的...\
用兩個三角形拼湊成一個方形。

![首先是第一個三角形](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-46.png)

```css
background: #eee;
background-image:
 linear-gradient(45deg, #bbb 25%, transparent 0);
background-size: 30px 30px;/*寬高*/
```

![另外一邊的三角形..](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-47.png)

```css
background: #eee;
background-image:
 linear-gradient(45deg, transparent 75%, #bbb 0);
background-size: 30px 30px;
```

![合併兩個三角形](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-48.png)

```css
background: #eee;
background-image:
 linear-gradient(45deg, #bbb 25%, transparent 0),
 linear-gradient(45deg, transparent 75%, #bbb 0);
background-size: 30px 30px;
```

![background-position↘](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-49.png)

```css
background: #eee;
background-image:
 linear-gradient(45deg, #bbb 25%, transparent 0),
 linear-gradient(45deg, transparent 75%, #bbb 0);
background-position: 0 0, 15px 15px;/*x軸y軸*/
background-size: 30px 30px;/*寬高*/
```

![再增加兩個漸層，然後賦予定位，就完成了...](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-44.png)

```css
background-image:
 linear-gradient(45deg, #bbb 25%, transparent 0),
 linear-gradient(45deg, transparent 75%, #bbb 0),
 linear-gradient(45deg, #bbb 25%, transparent 0),
 linear-gradient(45deg, transparent 75%, #bbb 0);
background-position: 0 0, 15px 15px, 15px 15px, 30px 30px;
background-size: 30px 30px;
```

### 然後下面是Sass的寫法

```css
@mixin checkerboard($size, $base,
 $accent: rgba(0,0,0,.25) {
   background: $base;
   background-image:
 linear-gradient(45deg,
 $accent 25%, transparent 0,
 transparent 75%, $accent 0),
 linear-gradient(45deg,
 $accent 25%, transparent 0,
 transparent 75%, $accent 0);
background-position: 0 0, $size $size,
 background-size: 2*$size 2*$size;
}
/* Used like… */
@include checkerboard(15px, #58a, tan);
```

### 下面是SVG

```markup
<svg xmlns="http://www.w3.org/2000/svg"
 width="100" height="100" fill-opacity=".25" >
<rect x="50" width="50" height="50" />
<rect y="50" width="50" height="50" />
</svg>
```

抱歉我看不懂，我就只剩下paste了🤪

```markup
background: #eee url('data:image/svg+xml,\
 <svg xmlns="http://www.w3.org/2000/svg" \
 width="100" height="100"
 fill-opacity=".25">\
 <rect x="50" width="50" height="50" /> \ 
<rect y="50" width="50" height="50" /> \
 </svg>');
background-size: 30px 30px;
```


{% endtab %}

{% tab title="疊加效果?" %}
「background-blend-mode」，我甚麼都不知道，我就只管貼上而已XD\
這些圖案大多只使用了「multiply」疊加模式。 \
另外還有「overlay」「screen」「difference」

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-51.png)


{% endtab %}
{% endtabs %}

## 【07－隨機背景】

「linear-gradient」

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-55.png)

{% tabs %}
{% tab title="原本的" %}
\#fb3是黃色、#655是褐色、#ab4是黃綠色、hsl的那個是鵝黃色。

![中規中矩](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-53.png)

```css
background: linear-gradient(90deg,
                #fb3 15%, #655 0, #655 40%,
                 #ab4 0, #ab4 65%, hsl(20, 40%, 90%) 0);
background-size: 80px 100%;
```


{% endtab %}

{% tab title="稍微變化" %}
使用透明顏色疊加顏色。

![可是還是看得出規律](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-54.png)

```css
background: hsl(20, 40%, 90%);
background-image:
 linear-gradient(90deg, #fb3 10px, transparent 0),
 linear-gradient(90deg, #ab4 20px, transparent 0),
 linear-gradient(90deg, #655 20px, transparent 0);
background-size: 80px 100%, 60px 100%, 40px 100%;
```
{% endtab %}

{% tab title="很長" %}
很大的空間才能看出變化

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-55.png)

```css
background: hsl(20, 40%, 90%);
background-image:
 linear-gradient(90deg, #fb3 11px, transparent 0),
 linear-gradient(90deg, #ab4 23px, transparent 0),
 linear-gradient(90deg, #655 41px, transparent 0);
background-size: 41px 100%, 61px 100%, 83px 100%;
```
{% endtab %}
{% endtabs %}



## 【08－圖片邊框】

「border-image」\[[原網址](https://www.w3cplus.com/css3/css-secrets/continuous-image-borders.html)]

![](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-57.png)

{% tabs %}
{% tab title="border-image" %}
![](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-58.png)


{% endtab %}

{% tab title="信封邊框" %}
![](https://www.w3cplus.com/sites/default/files/blogs/2015/1509/css-secrets-61.png)

```css
{
  padding: 1em; 
  border: 1em solid transparent; 
  background: linear-gradient(white, white) padding-box,
    repeating-linear-gradient(-45deg, red 0, red 12.5%, 
                              transparent 0, transparent 25%, #58a 0, #58a 37.5%,
                              transparent 0, transparent 50%) 0 / 5em 5em;
}
```

```css
{
  padding: 1em; 
  border: 16px solid transparent; 
  border-image: 16 
    repeating-linear-gradient(-45deg, red 0, red 1em, 
                              transparent 0, transparent 2em, 
                              #58a 0, #58a 3em, 
                              transparent 0, transparent 4em);
}
```
{% endtab %}
{% endtabs %}













