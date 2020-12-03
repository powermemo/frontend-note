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

Zebra-striped text lines p.214\[[原網址](https://www.w3cplus.com/css3/css-secrets/zebra-strlped-text-lines.html)\] \| codepen22

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

