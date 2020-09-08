# 壞了，我的醫生

![](https://scontent.ftpe8-1.fna.fbcdn.net/v/t1.0-9/22688337_373357853121512_1359550471304573685_n.png?_nc_cat=105&_nc_sid=09cbfe&_nc_ohc=PYhES7me9w8AX8uC9UA&_nc_ht=scontent.ftpe8-1.fna&oh=ae50ca5a806320eac362dfe47726d524&oe=5F7A59F7)

## jQuery

### 動畫莫名其妙延遲

不知道為什麼動畫進行，執行某些動作後function便會故障或是延遲幾秒才執行。  
\[[How to prevent this strange jQuery .animate\(\) lag?](https://stackoverflow.com/questions/14613498/how-to-prevent-this-strange-jquery-animate-lag)\]

```javascript
//🟡在.animate()前加入「.stop()」
$("#newResForm").stop().animate({ opacity: 0 }, 100,function() {
   $("#newResFormWrap").toggle('fast', function (){
       $("#addRes").animate({ opacity: 100 }); 
           // ...
```

## JS

### 怎麼知道scrollbar的寬度

滿版區域一直會凸出去產生水平卷軸...\(多出window的chorme卷軸寬度17px\)。  
不用算，直接用裏面寬度去決定滿版的寬度。  
`document.documentElement.clientWidth`  
\[[Get scrollbar width in JavaScript](https://muffinman.io/get-scrollbar-width-in-javascript/)\]

```javascript
//算出scrollbar寬度。
function getScrollbarWidth() {
  return window.innerWidth - document.documentElement.clientWidth;
}
```

