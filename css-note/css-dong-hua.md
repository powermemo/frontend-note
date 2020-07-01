---
description: 參考其他網頁再由自己的方法記下^_^。
---

# CSS動畫

[CSS3動畫快速入門](https://eyesofkids.gitbooks.io/css3/contents/intro.html)  
[CSS 3D cube](https://www.smashingmagazine.com/2016/07/front-end-challenge-accepted-css-3d-cube/)  
[OXXO Studio](https://www.oxxostudio.tw/articles/201506/css-3d.html)

## 簡介

### ■ 分類

CSS3動畫分為兩種

* transitions 轉場
* animation 動畫

### ■ 與JS比較，CSS3動畫

簡單、低效能、最佳化（流暢）

### ■ 轉場 & 動畫的不同

{% tabs %}
{% tab title="觸發" %}
觸發方式（trigger）

* transition要透過事件（例如:hover）帶動。
* animation不用，一進入頁面就可以開始。 （要加hover之類的帶動也是可以）
{% endtab %}

{% tab title="循環" %}
循環 / 重複 （Looping）

* transition沒有。
* animation有。animation-iteration-count 可以撤定循環次數，或「infinite\(無限\)」重複。
{% endtab %}

{% tab title="關鍵影格" %}
關鍵影格（keyframes）

* transition沒有。
* animation有。可以做更複雜的效果。
{% endtab %}

{% tab title="JS互動" %}
transition和animation皆可以與JS作互動。

* transition容易。
* animation不易。
{% endtab %}

{% tab title="相容性" %}
* transition 九成以上瀏覽器可支援。
* animation與transition狀況相似。
{% endtab %}
{% endtabs %}



## transition 轉場

有**四個屬性**，這些屬性可以合併到一個transition屬性中。

{% tabs %}
{% tab title="-property" %}
**transition-property**，  
定義那些CSS屬性會被影響，例如background-color。  
default是「all」，但也不是所有的CSS屬性都可以使用transition。 - [可用清單](https://www.w3.org/TR/2009/WD-css3-transitions-20091201/#animatable-properties-) -   
以下隨意的範例：

```css
.box{
    transition-property: background-color;
}
```
{% endtab %}

{% tab title="★-duration" %}
**transition-duration** ， 單位「s」秒  
定義持續時間，default是「`0s`」。  
以下隨意舉例：

```css
.box{
    transition-duration: 2s;
}
```
{% endtab %}

{% tab title="-timing-function" %}
**transition-timing-function** ，  
時間函數，設定貝茲曲線。  
 - [各種示範](https://developer.mozilla.org/en-US/docs/Web/CSS/transition-timing-function) -   
以下列出部分內容。

* ease \(default\)
* linear
* ease-in
* ease-out
* ease-in-out
* cubic-bezier\(\)   \[[樣式清單](https://matthewlein.com/tools/ceaser)\]  \[[客製化貝茲](https://cubic-bezier.com/) \]

以下隨意舉例：

```css
.box{
    transition-timing-function: linear;
}
```
{% endtab %}

{% tab title="-delay" %}
**transition-delay** ，單位「s」秒  
定義延遲開始時間，default「`0s`」。  
以下隨意舉例：

```css
.box{
    transition-delay: 1s;
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
口訣：「手續被延」→「**屬**性、持**續、貝**茲、**延**遲」
{% endhint %}

transition的必填與選填：常見Amos的transition只加入秒數。  
`transition: 5s` 等同於 `transition: all .5s ease;`。



## animation 動畫

\[[OXXO的詳細解說](https://www.oxxostudio.tw/articles/201803/css-animation.html)\]

### ■ keyframes關鍵影格

起手式－keyframes。0%～100%，  
也可以用名稱「from」（0%）以及「to」（100%）表示。

{% tabs %}
{% tab title="起手式" %}
```css
@keyframes oxxo{
    from{left:0;}
    to{left:100px;}
}
```
{% endtab %}

{% tab title="另一種寫法" %}
```css
@keyframes xxxx{
    0%{left:0;}
    100%{left:100px;}
}
```
{% endtab %}
{% endtabs %}



### ■ animation屬性

animation有**八個屬性**，這些屬性可以合併到一個animation屬性中。

{% tabs %}
{% tab title="name" %}
**animation-name，**定義keyframe的名稱。

* transition則是transition-property定義套用的屬性。
{% endtab %}

{% tab title="-duration" %}
**animation-duration**，持續期間，default「`0s`」。

* 與transition-duration一樣。
{% endtab %}

{% tab title="-time-function" %}
**animation-time-function**，時間函數（貝茲），default「`ease`」。

* 與transition-time-function相似。
* step\(禎數,start\)
* step-end\(禎數,end\)
{% endtab %}

{% tab title="-delay" %}
**animation-delay**，延遲開始時間，default「`0s`」。

* 與transition-delay一樣。
{% endtab %}

{% tab title="-iteration-count" %}
**animation-iteration-count**，撥放循環次數，default「`1`」。  
可以設定「`infinite`」，代表無限次數撥放。
{% endtab %}

{% tab title="-direction" %}
**animation-direction**，播放方向。

* normal
* reverse（反向／倒帶）
* alternate（輪流）
* alternate-reverse（輪流與反向）
{% endtab %}

{% tab title="-fill-mode" %}
**animation-fill-mode**，播放後樣式。default「`none`」。

* none（default）
* forwards停留在最後的樣式。
* backwards一開始的樣式。
* both兩者都套用

❗ 會因animation-direction的值而不同。
{% endtab %}

{% tab title="-play-state" %}
**animation-play-state**，播放狀態。default「`running`」。

* running﹙default﹚ ▶ 
* paused暫停播放 ⏸ 
{% endtab %}
{% endtabs %}

套用animation：  
讓「同一個元素套用多組動畫」，用法只需要在後方用逗點「,」分隔即可。

{% tabs %}
{% tab title="格式" %}
```css
animation:name duration | timing-function | delay | iteration-count | direction | 
fill-mode | play-state;
```
{% endtab %}

{% tab title="舉例" %}
```css
.box{
    animation: xxxx 5s infinite linear,
		        　　oxxo 3s 5 ease;
}//這個範例共用了兩組動畫。
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
口訣：「名詞支援次方衝撞」  
　　　→「**名**稱、**持**續、貝**茲**、**延**遲、**次**數、**方**向、填**充**\(最後樣式\)、**狀**態\(⏯\)」
{% endhint %}



### 

### 





### ■ 一些動畫範例

\[[OOXX多邊形教學](https://www.oxxostudio.tw/articles/201503/css-regular-polygon-transform.html)\]

{% tabs %}
{% tab title="Cube" %}
{% embed url="https://codepen.io/eyesofkids/pen/VKkXmE" caption="https://codepen.io/eyesofkids/pen/VKkXmE" %}
{% endtab %}

{% tab title="Loading" %}
我還沒搞懂==，反正它還有點怪怪的... \[[作者連結](https://www.oxxostudio.tw/articles/201406/css-google-loading.html)\]

{% embed url="https://codepen.io/ch-zhuchu/pen/oNjaYrP" caption="https://codepen.io/ch-zhuchu/pen/oNjaYrP" %}
{% endtab %}

{% tab title="Triangle" %}
* 三角形由邊框組成，改變的是border而不是background。

啊它也怪怪的==...\[[作者連結](https://www.oxxostudio.tw/articles/201506/css-3d-platonic-solid-1.html)\]

{% embed url="https://codepen.io/ch-zhuchu/pen/gOaBgwO" caption="https://codepen.io/ch-zhuchu/pen/gOaBgwO" %}
{% endtab %}

{% tab title="Daimend" %}
\[[作者連結](https://www.oxxostudio.tw/articles/201506/css-3d-platonic-solid-2.html)\]

{% embed url="https://codepen.io/ch-zhuchu/pen/ExVdZWR" caption="https://codepen.io/ch-zhuchu/pen/ExVdZWR" %}
{% endtab %}

{% tab title="dodecahedron" %}
\[[作者連結](https://www.oxxostudio.tw/articles/201506/css-3d-platonic-solid-2.html)\]

{% embed url="https://codepen.io/ch-zhuchu/pen/qBOJRjL" caption="https://codepen.io/ch-zhuchu/pen/qBOJRjL" %}
{% endtab %}
{% endtabs %}



## 



