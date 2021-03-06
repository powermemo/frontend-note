# CH07－結構與架構

## 【41－Sticky Footer】

![footer&#x61C9;&#x8A72;&#x8981;&#x5728;&#x9801;&#x9762;&#x6700;&#x5E95;&#x4E0B;&#x7684;&#xFF0C;&#x4F46;&#x5B83;&#x6C92;&#x6709;&#x3002;](https://www.w3cplus.com/sites/default/files/blogs/2015/1507/css-secrets-7-22.png)

怎麼辦？\[[原連結](https://www.w3cplus.com/css3/css-secrets/sticky-footers.html)\]

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

2. 用**Flexbox**  
\(HTML與上方相同，我就不重複寫啦。\)

```css
body {
    display: flex;
    flex-flow: column;
    min-height: 100vh;
    }
main { flex: 1; }
```

{% hint style="info" %}
`flex`是`flex-grow`、`flex-shrink`、`flex-basis`的縮寫。  
 設定flex&gt;0，元素就會自行調配空間。   
例如&lt;main&gt;設定`flex:2`、&lt;footer&gt;設定`flex:1`，&lt;footer&gt;的高度是&lt;main&gt;的1/2，
{% endhint %}

![&#x554F;&#x984C;&#x89E3;&#x6C7A;&#xFF0C;&#x5B83;&#x5728;&#x6700;&#x4E0B;&#x9762;&#x4E86;&#x3002;](https://www.w3cplus.com/sites/default/files/blogs/2015/1507/css-secrets-7-24.png)

## 【】

