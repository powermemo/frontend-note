# transform

## transform 2D

transform並不是動畫屬性的一環，只是動畫很常使用它們（而且跟轉場單字很像XD）。  
它跟background-color等css是類似的東西。

{% tabs %}
{% tab title="scale" %}
**scale**縮放，單位「0~∞」倍數的概念。  
（打負號會轉180°縮放）

* scale\(\);  //若只給一組數字，表示x+y軸
* scaleX\(\);  
* scaleY\(\);
{% endtab %}

{% tab title="rotate" %}
**rotate**旋轉，單位「deg」度數。  
+deg順時鐘，-deg逆時鐘

* rotate\(+\)右轉　　\(-\)左轉
* rotateX\(+\)後轉　　\(-\)前轉
* rotateY\(+\)右轉　　\(-\)左轉

![&#x7531;&#x4E0A;&#x800C;&#x4E0B;&#x662F;&#x300C;rotate&#x300D;&#x300C;rotateX&#x300D;&#x300C;rotateY&#x300D;](../.gitbook/assets/image%20%2817%29.png)
{% endtab %}

{% tab title="translate" %}
**translate**平移，單位「px, em, in, %」等

* translate\(\)
* translateX\(\)
* translateY\(\)
{% endtab %}

{% tab title="skew" %}
**skew**傾斜，單位「deg」。

* skew\(\)
* skewX\(\)
* skewY\(\)
{% endtab %}
{% endtabs %}

{% hint style="info" %}
可套用多組（以空格區隔）  
例如：`transform: rotate(45deg) translateX(200px);`
{% endhint %}

### transform-origin 變形原點

transform-origin變形原點，用名稱或百分比%改變 **變形的基準點**。  
X軸　top（0）/center（50%）/bottom（100%）  
Y軸　left（0）/center（50%）/right（100%）

* transform-origin:$$x$$ $$y$$;  //「x」填入x軸位置；「y」填入y軸位置。



## transform 3D

### perspective透視點

perspective透視點/消失點，代表**Z軸**。沒了這個就無法驅動Z軸。  
perspective是指，**鏡頭到透視點的距離**。  
500px~1000px是中等範圍（失真中等）

共有兩種設定方式：

* `perspective: 500px;`
* `transform: perspective(500px);`

{% hint style="info" %}
z軸數字越大，距離螢幕越近（圖像越大）。  
z軸數字≧perspective，圖像就會消失（超出螢幕了）。
{% endhint %}

{% tabs %}
{% tab title="translateZ" %}
perspective加上translateZ  
下方圖例：  
左邊`transform: perspective(250px)  translateZ(-50px);`  
右邊`transform: perspective(250px)  translateZ(50px);`

![https://codepen.io/eyesofkids/pen/WGZraq](../.gitbook/assets/image%20%288%29.png)
{% endtab %}

{% tab title="rotateXYZ" %}
perspective加上rotateXYZ  
下方圖例：  
左邊`transform: perspective(250px) rotateX(45deg);`  
中間`transform: perspective(250px) rotateY(45deg);`  
右邊`transform: perspective(250px) rotateZ(45deg);`

![rotateX / rotateY / rotateZ](../.gitbook/assets/image%20%2814%29.png)
{% endtab %}
{% endtabs %}



### perspective-origin改變透視點位置

perspective-origin改變透視點\(消失點\)位置，它是x軸&y軸，與transform-origin的概念雷同。  
X軸　top（0）/center（50%）/bottom（100%）  
Y軸　left（0）/center（50%）/right（100%）



### perspective-matrix透視矩陣

perspective + perspective-origin → perspective-matrix

![&#x8CC7;&#x6599;&#x4F86;&#x6E90;&#xFF1A;CSS 3D cube](../.gitbook/assets/image%20%286%29.png)

### backface-visibility

3D圖像中，被擋住的部分要不要看見？default「`hidden`」。「`visible`」可視

![&#x5DE6;&#x908A;backface-visibility: hidden; &#x53F3;&#x908A;backface-visibility: visible;](../.gitbook/assets/image%20%2824%29.png)



