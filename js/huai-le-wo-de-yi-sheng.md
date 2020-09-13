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
//❌❌❌沒有，沒有正常！
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

#### jQuery傳值給PHP\(POST\)

\[[jquery與php傳值篇](https://ithelp.ithome.com.tw/articles/10160671)\]

{% tabs %}
{% tab title="jQuery" %}
```javascript
<script>
    $(function(){
      $.post('url.php',{id:<?=$id;?>},function(data){
        alert(data);
      });
    });
</script>
/************** or ****************/
<script>
    $(function(){
    var id = $('input[name="test"]').val();
      $.post('url.php',{id:id},function(data){
        alert(data);
      });
    });
</script>
<input type="hidden" name="test" value="2">
```
{% endtab %}

{% tab title="PHP" %}
```php
//url.php
<?php
    $id = $_POST['id'];
    if($id == 2):
      echo "ok";
    else:
      echo "no";
    endif;
?>
```
{% endtab %}
{% endtabs %}

## JS

### 基礎

{% tabs %}
{% tab title="boolean變數字" %}
#### boolean的值怎麼變數字（給1\|0）

\[[Convert boolean result into number/integer](https://stackoverflow.com/questions/7820683/convert-boolean-result-into-number-integer)\]

```javascript
let chc = document.querySelectorAll('input[type=checkbox]');
chc.forEach(data => data.checked==true ? data.value=1 : data.value=0)
```
{% endtab %}

{% tab title="input\[required\]的數量" %}
#### 怎麼計算input\[required\]的數量

\[[get required form elements via DOM in javascript](https://stackoverflow.com/questions/35396980/get-required-form-elements-via-dom-in-javascript)\]

```javascript
document.querySelectorAll('[required]').length;
```

#### 進階：JS指令「沒填完不准走」

```php
<input type="text"required>
<input type="text"required>
<button type="button" id="bara" disabled>click</button>
<script>
  document.querySelector('#bara').addEventListener('click',function(){
    let elm = document.querySelectorAll('[required]');
    let elmlen = elm.length
    let empnum = 0; 
    for(let i=0;i<elmlen;i++){
      if(elm[i].value==""){empnum+=1}
    }
    // empnum==0?alert('yeah'):alert('no');
    //另一種
    if(empnum==0){alert('yeah')}
    else{alert('no')}
  })
</script>
```

```php
//沒填粉紅色，有點沒粉紅
<input type="text"required>
<input type="text"required>
<button type="button" id="bara">click</button>
<script>
  let elm = document.querySelectorAll('[required]');
  let elmlen = elm.length
  document.querySelector('#bara').addEventListener('click',function(){
    let empnum = 0; 
    for(let i=0;i<elmlen;i++){
      if(elm[i].value==""){//如果表格沒填
        empnum+=1;//計算沒填的表格
        elm[i].classList.add('noucant')//背景變成粉紅色
      }else{//有填表格
        elm[i].classList.remove('noucant')//去除粉紅色
      }
    }
    if(empnum==0){alert('yeah')}
    else{ alert('no')}
  })
  for(let i=0;i<elmlen;i++){
    elm[i].addEventListener('change',function(){
      if(elm[i].value==""){elm[i].classList.add('noucant')}
      else{elm[i].classList.remove('noucant')}
    })
  }
</script>
```
{% endtab %}
{% endtabs %}

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

#### 要怎麼動態新增變數

用`eval()`。這個函數是將傳入的字符串當做JavaScript 代碼進行執行。  
\[[How to use dynamic variable names in JavaScript ?](https://www.geeksforgeeks.org/how-to-use-dynamic-variable-names-in-javascript/)\]

```javascript
var k = 'value'; 
var i = 0; 
for(i = 1; i < 5; i++) { 
    eval('var ' + k + i + '= ' + i + ';'); 
} 
console.log("value1=" + value1); 
console.log("value2=" + value2); 
console.log("value3=" + value3); 
console.log("value4=" + value4); 
//【result】value1=1
//【result】value2=2
//【result】value3=3
//【result】value4=4
```

#### javasript傳值給php\(GET\)

\[[\[js\] JS 與 PHP 傳值](https://medium.com/@jacobhsu/js-js-%E8%88%87-php-%E5%82%B3%E5%80%BC-983faf68804b)\]

```javascript
<script>
function express(){
    var value="abc";
    location.href="point.php?value=" +value;
}
</script>

<button onclick="express()"></button>
<?php
    echo $_GET['value'];
?>
```



## PHP

#### 要怎麼動態新增變數

用字串的方式「`{.}`」  
\[[Using braces with dynamic variable names in PHP](https://stackoverflow.com/questions/9257505/using-braces-with-dynamic-variable-names-in-php)\]

```javascript
for($i=0; $i<=2; $i++) {
   ${"file" . $i} = file($filelist[$i]);
}
```

#### php傳值給javascript

\[[\[js\] JS 與 PHP 傳值](https://medium.com/@jacobhsu/js-js-%E8%88%87-php-%E5%82%B3%E5%80%BC-983faf68804b)\]

```javascript
<?php
    $value="abc";
?>

<script>
    var value="<?=$value; ?>";
    document.write(value);
</script>
```

#### checkbox沒被選取，PHP顯示undefined

\[[Undefined Index If I Do Not Check Checkbox](https://stackoverflow.com/questions/18603884/undefined-index-if-i-do-not-check-checkbox/18603899#18603899)\]

 You have to use `isset($_POST['publishok'])` to check it whether it is checked in the server side.

```php
echo isset($_REQUEST['e']) ? 1 : 0;
```

