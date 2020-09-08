# 壞了，我的醫生

![](https://scontent.ftpe8-1.fna.fbcdn.net/v/t1.0-9/22688337_373357853121512_1359550471304573685_n.png?_nc_cat=105&_nc_sid=09cbfe&_nc_ohc=PYhES7me9w8AX8uC9UA&_nc_ht=scontent.ftpe8-1.fna&oh=ae50ca5a806320eac362dfe47726d524&oe=5F7A59F7)

## jQuery

#### 動畫莫名其妙延遲

不知道為什麼動畫進行，執行某些動作後function便會故障或是延遲幾秒才執行。  
\[[How to prevent this strange jQuery .animate\(\) lag?](https://stackoverflow.com/questions/14613498/how-to-prevent-this-strange-jquery-animate-lag)\]

```javascript
//🟡在.animate()前加入「.stop()」
$("#newResForm").stop().animate({ opacity: 0 }, 100,function() {
   $("#newResFormWrap").toggle('fast', function (){
       $("#addRes").animate({ opacity: 100 }); 
           // ...
```

#### hover控制setInterval和clearInterval

hover之後，閒置一段時間，動畫不受控地快轉。  
`❌setInterval(()=>{fn()},time)  
✅setInterval(fn,time)`  
\[[Adding pause on hover to setInterval\(\)?](https://stackoverflow.com/questions/10913703/adding-pause-on-hover-to-setinterval)\]

{% tabs %}
{% tab title="\(不是重點\)動畫函式" %}
```javascript
function moveRight3() {            //向右走
  $('.slider3 .slides').animate({
    left: - slideWidth3
  }, 300, function () {
    $('.slider3 .slides li:first-child').appendTo('.slider3 .slides');
    $('.slider3 .slides').css('left', '');
    currentLi3 = parseInt($('.slider3 ul li').eq(1).attr('data-page'));//目前slide在第幾頁(數值)
    currentDot3 = $('.steps3 li').eq(currentLi3-1);           //目前的點點在第幾個(物件)
    dotColorChange3()
  });
};
```
{% endtab %}

{% tab title="原本長這樣" %}
```javascript
//load後自動輪播
timeId3=setInterval( ()=> { moveRight3() , 3500});
//hover
$('.news .section').hover(
  function(){                   //滑到的時候
  clearInterval(timeId3)          //停止動畫
}, function(){                  //滑出的時候
  timeId3=setInterval( ()=> { moveRight3() , 3500});//再啟動動畫
});
```
{% endtab %}

{% tab title="調整後好像正常了" %}
```javascript
//load後自動輪播  //🟡👇調整了下面
timeId3=setInterval(   moveRight3 , 3500);
//hover
$('.news .section').hover(
  function(){                   //滑到的時候
  clearInterval(timeId3)          //停止動畫
}, function(){                  //滑出的時候
  //🟡👇調整了下面
  timeId3=setInterval(   moveRight3 , 3500);//再啟動動畫
});
```
{% endtab %}
{% endtabs %}

## JS

#### 怎麼知道scrollbar的寬度

滿版區域一直會凸出去產生水平卷軸...\(多出window的chorme卷軸寬度17px\)。  
**不用算**，直接用裏面寬度去決定滿版的寬度。  
`document.documentElement.clientWidth`  
\[[Get scrollbar width in JavaScript](https://muffinman.io/get-scrollbar-width-in-javascript/)\]

```javascript
//算出scrollbar寬度。
function getScrollbarWidth() {
  return window.innerWidth - document.documentElement.clientWidth;
}
```

