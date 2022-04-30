# CH07－結構與架構

## 【36內容尺寸】

Intrinsic sizing p.298\[[原網址](https://www.w3cplus.com/css3/css-secrets/intrinsic-sizing.html)]

## 【37表格直欄寬】

Taming table column widths p.302\[[原網址](https://www.w3cplus.com/css3/css-secrets/taming-table-column-widths.html)]

## 【38相鄰元素樣式】

Styling by sibling count p.306\[[原網址](https://www.w3cplus.com/css3/css-secrets/styling-by-sibling-count.html)]

## 【39流體背景固定內容】

Fluid background fixed content     p.312\[[原網址](https://www.w3cplus.com/css3/css-secrets/fluid-background-fixed-content.html)]

## 【40垂直居中】

Vertical centering p.316 \[[原網址](https://www.w3cplus.com/css3/css-secrets/vertical-centering.html)]

## 【41－Sticky Footer】

![footer應該要在頁面最底下的，但它沒有。](https://www.w3cplus.com/sites/default/files/blogs/2015/1507/css-secrets-7-22.png)

怎麼辦？\[[原連結](https://www.w3cplus.com/css3/css-secrets/sticky-footers.html)]

1.用**計算的**

{% tabs %}
{% tab title="HTML" %}
```markup
<header>
    <h1>Site name</h1>
</header>
<main>
    <p>Bacon Ipsum dolor sit amet…
    <!-- Filler text from baconipsum.com --></p>
</main>
<footer>
    <p>© 2015 No rights reserved.</p>
    <p>Made with ♥ by an anonymous pastafarian.</p>
</footer>
```
{% endtab %}

{% tab title="修改CSS" %}
```css
main {
    min-height: calc(100vh - 2.5em - 7em);
    /* Avoid padding/borders screwing up our height: */
    box-sizing: border-box;
}
```
{% endtab %}

{% tab title="另一種方法" %}
```css
/*HTML的部分，要先將<head>和<main>包起來*/
#wrapper {
    min-height: calc(100vh - 7em);
}
```
{% endtab %}
{% endtabs %}

2\. 用**Flexbox**\
(HTML與上方相同，我就不重複寫啦。)

```css
body {
    display: flex;
    flex-flow: column;
    min-height: 100vh;
    }
main { flex: 1; }
```

{% hint style="info" %}
`flex`是`flex-grow`、`flex-shrink`、`flex-basis`的縮寫。\
&#x20;設定flex>0，元素就會自行調配空間。 \
例如\<main>設定`flex:2`、\<footer>設定`flex:1`，\<footer>的高度是\<main>的1/2，
{% endhint %}

![問題解決，它在最下面了。](https://www.w3cplus.com/sites/default/files/blogs/2015/1507/css-secrets-7-24.png)

