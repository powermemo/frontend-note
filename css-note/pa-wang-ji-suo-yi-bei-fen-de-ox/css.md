# CSS

## CSS黏黏球

教學網址\[[連結](https://www.oxxostudio.tw/articles/201408/sticky-ball.html)\] \[[EZoA](https://jqmdesigner.appspot.com/designer.html#&id=1592100727213)\]

### PS裡的效果

{% tabs %}
{% tab title="IMG" %}
![](https://www.oxxostudio.tw/img/articles/201408/20140829_1_06.gif)
{% endtab %}

{% tab title="操作" %}
![&#x5206;&#x5716;&#x5C64;\(div\)&#x5EFA;&#x7ACB;&#x5713;&#x5708;](https://www.oxxostudio.tw/img/articles/201408/20140829_1_02.png)

![&#x9AD8;&#x65AF;&#x6A21;&#x7CCA;&#x6548;&#x679C;](https://www.oxxostudio.tw/img/articles/201408/20140829_1_04.png)

![&#x300C;&#x5EFA;&#x7ACB;&#x65B0;&#x586B;&#x8272;&#x6216;&#x8ABF;&#x6574;&#x5716;&#x5C64;&#x300D;&#x4EAE;&#x5EA6;&#x5C0D;&#x6BD4;&#xFF0C;&#x4F7F;&#x7528;&#x820A;&#x7248;](https://www.oxxostudio.tw/img/articles/201408/20140829_1_05.png)
{% endtab %}
{% endtabs %}

### CSS

**模糊**的濾鏡必須使用`-webkit-filter:blur(數值)`  
**對比**則使用`-webkit-filter:contrast(數值)`  
這個只能夠運行在 Chrome 和 Safari 

![](https://www.oxxostudio.tw/img/articles/201408/20140829_1_07.gif)

{% tabs %}
{% tab title="HTML" %}
```markup
<div class="effect">
  <div class="blackball"></div>
  <div class="redball"></div>
</div>
```
{% endtab %}

{% tab title="CSS" %}
```css
.effect{
  width:100%;
  height:100%;
  padding-top:50px;
  -webkit-filter:contrast(10);/*🔸對比*/
  background:#fff;
}
.blackball,
.redball{
  padding:10px;
  border-radius:50%;
  -webkit-filter:blur(5px);/*🔸模糊*/
}
.blackball{
  width:100px;
  height:100px;
  background:black;
  margin:0 auto;
  z-index:1;
}
.redball{
  width:60px;
  height:60px;
  background:red;
  position:absolute;
  top:70px;
  left:50px;
  z-index:2;
  -webkit-animation:rball 6s infinite;
}
```
{% endtab %}

{% tab title="動畫CSS" %}
```css
@-webkit-keyframes rball{
  0%,100%{
    left:35px;
    width:60px;
    height:60px;
  }
  4%,54%{
    width:60px;
    height:60px;
  }
  10%,60%{
    width:50px;
    height:70px;
  }
  20%,70%{
    width:60px;
    height:60px;
  }
  34%,90%{
    width:70px;
    height:50px;
  }
  41%{
    width:60px;
    height:60px;
  }
  50%{
    left:calc(100% - 95px);
    width:60px;
    height:60px;
  }
}
/*所以要測試的話，最外層的 effect 寬度記得設為 320px*/
```
{% endtab %}

{% tab title="另一款籃球CSS" %}
```css
.blueball1{
  width:80px;
  height:80px;
  background:#00f;
  padding:10px;
  border-radius:50%;
  position:absolute;
  top:230px;
  left:0;
  z-index:2;
  -webkit-filter:blur(8px) ;
  -webkit-animation:bball1 6s infinite;
}
.blueball2{
  width:80px;
  height:80px;
  background:#00f;
  padding:10px;
  border-radius:50%;
  position:absolute;
  top:230px;
  left:240px;
  z-index:2;
  -webkit-filter:blur(8px) ;
  -webkit-animation:bball2 6s infinite;
}
@-webkit-keyframes bball1{
  0%,100%{
    left:0;
    top:230px;
    width:80px;
    height:80px;
  }
  20%{
    top:230px;
    width:80px;
    height:80px;
  }
  85%{
    top:230px;
    left:75px;
    width:90px;
    height:70px;
  }
  90%{
    top:228px;
    width:75px;
    height:85px;
  }
  50%{
    top:215px;
    left:110px;
    width:110px;
    height:110px;
  }
}
@-webkit-keyframes bball2{
  0%,100%{
    left:240px;
    top:230px;
    width:80px;
    height:80px;
  }
  20%{
    top:230px;
    width:80px;
    height:80px;
  }
  85%{
    top:230px;
    left:165px;
    width:90px;
    height:70px;
  }
  90%{
    top:228px;
    width:75px;
    height:85px;
  }
  50%{
    left:110px;
    top:215px;
    width:110px;
    height:110px;
  }
}
```
{% endtab %}
{% endtabs %}

