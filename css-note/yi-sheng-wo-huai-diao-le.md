---
description: 雜症處理區。
---

# 醫生，我壞掉了

![Excuse me?](https://dvblobcdnjp.azureedge.net/Content/Upload/Popular/Images/2017-06/e99e6b5e-ca6c-4c19-87b7-dfd63db6381a\_m.jpg)

## 動畫

### animation動畫動不了

* [ ] @keyframes腳本與 animation屬性是一組的，但不能打在一起。
* [ ] 你確定你的CSS屬性、定義的名稱都有拚對嗎？
* [ ] 你確定語法、標點符號有使用正確嗎？
* [ ] 你的CSS有放對地方嗎？沒有不小心打在其他人家裡面？字沒有貼邊

## 定位

### absolute的字沒有貼邊(其實問題是transform)

這是個案....，這影響到旋轉的問題...\


![對齊貼邊「absolute」「rotate」「transform-origin」](<../.gitbook/assets/image (23).png>)

* 好幾個內容與相對應的側邊字。\
  內容設定「relative」，側邊字設定「absolute」
* 側邊字旋轉「rotate(-90deg)」
* 每個內容的側邊字的偏移位置不一。
* ❗解決❗ 沒有設定到「transform-origin」，\
  每個側邊字都是由自己的中心點旋轉，所以偏移的位置才會不一樣。

{% tabs %}
{% tab title="HTML" %}
```markup
<div class="wrap">
  <div class="sidtt">
    aaaaa
  </div>
</div>
<div class="wrap">
  <div class="sidtt">
    ccccccccccc
  </div>
</div>
```
{% endtab %}

{% tab title="CSS(原始)" %}
```css
.wrap{/*這個區域都是樣式*/
  margin: 20px;
  width: 90%;
  height: 300px;
  border: 20px solid tomato;
}
.wrap{/*★★★★★定位調整★★★★★*/
  position:relative;
}
.sidtt{/*★★★★★定位調整★★★★★*/
  position:absolute;
  top:0px;
  right:0;
  transform:rotate(270deg);
}
```
{% endtab %}

{% tab title="CSS修改的部分" %}
```css
.sidtt{
  position:absolute;
  top:0px;
  right:0;
  transform:rotate(270deg);
  transform-origin: 100%  0; /*增加這個就不會有不同位置的問題了*/
}
```
{% endtab %}
{% endtabs %}

### absolute後內容被切半、字凸出去

![已經設定top:50%，冗贅→bottom:50%](<../.gitbook/assets/image (21).png>)

{% tabs %}
{% tab title="HTML" %}
```markup
<div class="wrap">
  <div class="btn">1235</div>
</div>
```
{% endtab %}

{% tab title="CSS" %}
```css
.wrap{
  position:relative;
  width: 90%;
  height: 350px;
  border: 5px solid #000;
}
.btn{/*定位*/
  position:absolute;
  top:50%;
/*   bottom: 50%; */ /*這是多餘的，不要用。*/
  right: 0;
}
.btn{/*這邊都是樣式*/
  font-size: 25px;
  color: white;
  font-weight: 900;
  background-color: tomato;
  padding: 15px;
  border-radius: 15px 15px 0 0;
  transform: rotate(-90deg) translate(100%,0);
  transform-origin:100% 100% ;
}

```
{% endtab %}
{% endtabs %}

## 圖片

### 自設透明圖片

本來使用「::before/::after」還有「absolute」，但是它們很難使用在RWD\
於是更換方法二：使用線性漸層「linear-gradient」+「::before/::after」

![](<../.gitbook/assets/image (29).png>)

{% embed url="https://bennettfeely.com/clippy/" %}

舉例（六角形）：

![](<../.gitbook/assets/image (32).png>)

```css
clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
```

### 正方形圖片，不設固定高的情況下

![目標：讓橘色(右方)圖片設定成正方形](<../.gitbook/assets/image (58).png>)

感謝兔子\~\~\~👍

```css
/*目標：讓橘色(右方)圖片設定成正方形*/
祖父層(整個橘色外框){
    /*如果不要圖片貼邊可以設定padding*/
}

父層(img的div框){
    padding-top: 20%;    /* 因為共有五個項目100% ÷ 5 = 20% */
    width: 20%;          /* padding-top設定甚麼就給甚麼 */
    position: relative;
    overflow: hidden;
}

img(子層){
    position: absolute;
    height: 100%;
    top: 50%;
    left: 0;
    transform: translateY(-50%);
}
```

## RWD

### 為什麼不作用？

權重問題！\
不管你「.main」是否後寫，\
「div.main」會一直大於「.main」。\
如果要RWD作用，就要打「div.main」（或是你前面都不要打「div.main」🤪）。

### 圖片太大，水平卷軸出現

我不想用`overflow:hidden;`，因為其他區域的東西會被切掉。

❗解決❗ 在「body」設定「`overflow-x:hidden;`」，這樣就不會有水平卷軸了！！

### 想做滿版的漢堡，但是區塊有被吃到

![](<../.gitbook/assets/image (34).png>)

感謝老師協助～\
問題在於，nav的高度是被nav裡面的項目撐開，\
若nav設定100vh，超出的範圍不會被看到（即使加入overflow=>scroll也會被吃掉空間的狀況）\
所以要**設定在nav的父層**。

{% tabs %}
{% tab title="HTML" %}
```markup
<div class="header">
  <div class="wrap">
    <div class="nav">
    <div class="logo"></div>
    <div class="ul">
      <li>1</li>
      <li>2</li>
    </div>
  </div>
  </div>
</div>





```
{% endtab %}

{% tab title="CSS" %}
```css
/*❌在.nav加入*/
.header .wrap .nav{
  overflow-y:scroll;
  height: 100vh;
}

/*⭕在.wrap加入*/
.header .wrap{
  overflow-y:scroll;
  height: 100vh;
}
```
{% endtab %}
{% endtabs %}

#### 燈箱的RWD也可以用相同作法\~\~

{% tabs %}
{% tab title="html" %}
```markup
<div class="wrap">
  <!--側邊攔-->
  <div class="sidenav">
    <ul><li></li></ul>
  </div>
  
  <!--🟡燈箱-->
  <div class="boxwrap">
    <div class="scrollwrap">
      <div class="box">
        <h3>小標1</h3>
        <input>
        <h3>小標2</h3>
        <input>
        <button class="open">關閉</button>
      </div>
    </div>
  </div>

  <!--主文-->
  <div class="main">
    <button class="open">打開</button>
    Lorem ipsum dolor sit amet.
  </div>
</div>
```
{% endtab %}

{% tab title="SCSS" %}
```css
.boxwrap{
  display:none;              //預設關閉狀態
  background: rgba(0,0,0,.6);//黑背景
  width: 100vw;              //滿版
  height: 100vh;             //滿版
  position: fixed;           //釘住
  flex-direction: column;    //以下燈箱置中樣式
  justify-content: center;
  align-items: center;
  text-align: center;
    
  .scrollwrap{
    margin: 25px 0;        //外面留空間
    overflow:auto;         //卷軸
    border-radius: 8px;    //倒圓角
    background: deeppink;  //背景色
    -ms-overflow-style: none;  //不要卷軸/* IE and Edge */
    scrollbar-width: none;     //不要卷軸/* Firefox */
    &::-webkit-scrollbar{display: none;}//不要卷軸
    
    .box{
      padding: 30px;     //以下燈箱內容置中調整
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
    }
    
  }
}
```
{% endtab %}

{% tab title="jq" %}
```javascript
//關閉 | 開啟
$('.open').click(function(){          //打開燈箱
  $('.boxwrap').css('display','');
  $('.boxwrap').css('display','fiex');
})
$('.close').click(function(){         //關閉燈箱
  $('.boxwrap').css('display','none');
})
```
{% endtab %}
{% endtabs %}

### 圖片蓋到連結，連結無法點擊

{% tabs %}
{% tab title="問題" %}
![](<../.gitbook/assets/image (33).png>)

上圖骨頭圖片PNG在最上層，紅框的部分是圖片所佔的範圍。\
因為被蓋到，綠色按鈕無法點擊。
{% endtab %}

{% tab title="解決問題" %}
![](<../.gitbook/assets/image (4).png>)

在圖片的CSS加入

`pointer-events: none;`

就可以「穿透」圖片，不點擊到他。
{% endtab %}
{% endtabs %}

### 內文死活都不肯換行

`white-space: pre;` 一點都不管用

```css
word-break: break-all;
```

