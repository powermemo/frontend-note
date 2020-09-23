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
\[[~~Adding pause on hover to setInterval\(\)?~~](https://stackoverflow.com/questions/10913703/adding-pause-on-hover-to-setinterval)~~\]~~

我用了bootstrap...

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

{% tab title="" %}
```

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
//(必填)沒填粉紅色，有點沒粉紅
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
非同步：\[[send json object from javascript to php](https://stackoverflow.com/questions/23750661/send-json-object-from-javascript-to-php/23750707)\]  \[[YOUTUBE](https://youtu.be/mNrJDGfQGz0?t=213)\]

{% tabs %}
{% tab title="傳旨給PHP" %}
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
{% endtab %}

{% tab title="把資料傳給PHP\(非同步\)" %}
```javascript
//JS檔案，以下所有「加密」「解密」純屬形容
var jsondata;
var flickr = {'action': 'Flickr', 'get':'getPublicPhotos'};
var data = JSON.stringify(flickr);            //加密，把↑物件轉JSON字串

var xhr = new XMLHttpRequest();
xhr.open("POST", "../phpincl/apiConnect.php", !0);
xhr.setRequestHeader("Content-Type", "application/json;charset=UTF-8");
xhr.send(data);                                //🟡1.把加密資料送給PHP
xhr.onreadystatechange = function () {
    if (xhr.readyState === 4 && xhr.status === 200) {
        // in case we reply back from server
        jsondata = JSON.parse(xhr.responseText);//🔰4.資料從PHP回來了，解密。
        console.log(jsondata);
    }
}

//PHP檔案
header('Content-type: application/json');
$json = file_get_contents('php://input');//🟡2.PHP收到JS的資料了
$json_decode = json_decode($json, true); //解密，第二個參數表示轉陣列非物件
$json_encode = json_encode($json_decode);//加密，轉JSON字串
echo $json_encode;                        //🔰3.資料傳回JS
```
{% endtab %}
{% endtabs %}

### 事件

#### wheel事件沒辦法做到[fullpage](https://alvarotrigo.com/fullPage/)的不閃跳

​我沒有百分之百清除，但降低很多\(頻率\)這樣的感覺。  
我用同學的方法：

* 靠DOM觸發滑動功能，而不是document,window等。
* 用一個「假標籤」滿版，先display:none，在滑動時顯示出來\(再消失\)。

{% tabs %}
{% tab title="架構" %}
這邊大致放一下，不是全部

```markup
<nav><ul><li></li></ul></nav>
<div class="section section1">
  <div class="animate">...</div>
  <!-- ↓防止滑動的空標籤 -->
  <div class="noScrollWell"></div>
  <!-- ↓下面這是輪播套件 -->
  <div id="carouselExampleCaptions" class="carousel slide" data-ride="carousel"></div>
  <button>scrollDown</button>
</div>
```
{% endtab %}

{% tab title="js" %}
我只要第一第二屏有效果、剩下的頁面不套用..

```php
function wheelDown(e)  {//🟡scroll down
  $(".noScrollWell").show();
  $('body,html').stop().animate({scrollTop: ww },800 ,
    function(){ $(".noScrollWell").hide(); }     //禁止滑動的牆壁消失
  )
}

function wheelUp(e){ //🟡scroll top
  $(".noScrollWell").show();
  $('body,html').stop().animate({scrollTop: '' },800,
    function(){ $(".noScrollWell").hide();}     //禁止滑動的牆壁消失
  )  
}

//🟡當我滾動滑鼠的時候
$('.container,#carouselExampleCaptions').on('wheel  DOMMouseScroll', function(e) { 
// $('.section1').on('scroll', function(e) { //當我滑動的時候
  // e.stopPropagation();
  // e.preventDefault();
  // e.stopImmediatePropagation(); 
  delta = e.originalEvent.deltaY;
  wheelhandler(e)
});

//🟡當阻絕的牆壁出現，停止一切scroll功能
$(".noScrollWell").on('scroll touchmove mousewheel', function(e){
  e.preventDefault();     
  e.stopPropagation();
  return false;
})

//🟡滑鼠事件
let sss=0 ;
function wheelhandler(e){
  delta = e.originalEvent.deltaY;
  if (delta > 0 && $(window).scrollTop() < ww/2) { //滑鼠往下滑  而且  <80
    clearTimeout(sss)
    sss=setTimeout(wheelDown(),800)
    e.preventDefault();    e.stopPropagation();//停止預設事件
  } else if(delta < 0 && ($(window).scrollTop() > $(window).scrollTop()/2 && $(window).scrollTop() <=ww)) {          
    clearTimeout(sss)
    sss= setTimeout(wheelUp(),800)                   //滑鼠往上滑 
    e.preventDefault();    e.stopPropagation();//停止預設事件
  }
  return false;
}
```
{% endtab %}
{% endtabs %}

### 非同步

#### 表單認證功能失效

{% tabs %}
{% tab title="問題" %}
input:email的格式、input\[required\]等等全都沒有用  
資料就這樣直接送去給PHP了！！
{% endtab %}

{% tab title="解方" %}
\[[checkValidity等form原生JS驗證方法和屬性詳細介紹](https://www.zhangxinxu.com/wordpress/2019/08/js-checkvalidity-setcustomvalidity/)\] \[[範例](https://codepen.io/nickleus/pen/qOjOGe)\]

用`checkValidity()`判斷  
用`reportValidity()`呼叫

```php
document.querySelector('#hibtn').addEventListener('click',function(e){
    var valid = this.form.checkValidity();//🟡
    if(valid){//🟢JS原生程式form判斷為true
      e.preventDefault();
      if(itsclose==false){
        changeVMfoData()//執行非同步function送出資料
        let reqElm = document.querySelectorAll('#class1 [required]')
        for(let i=0;i<reqElm.length;i++){
          itsclose = true;
          reqElm[i].disabled = true;
        }
      }
    }else{    //🟢JS原生程式form判斷為false
      //🟡這邊欄位若不符合設定的格式|規範就呼叫（例如：請填寫這個欄位）
      document.querySelector('[name="ven_email"]').reportValidity()
      document.querySelector('[name="ven_tel"]').reportValidity()
      document.querySelector('[name="ven_name"]').reportValidity()
    }
  })
```
{% endtab %}
{% endtabs %}

#### 奶奶的,我對非同步運作還是超級不熟

我放作品使用的使用者資料更改...

{% tabs %}
{% tab title="html" %}
```php
<div class="ven_information class" id="class1">
  <form class="all" method="POST">
      <div class="item">
          <span class="title">會員編號</span>
          <input class="content" disabled value="" name="ven_no">
      </div>
      <div class="item">
          <span class="title">帳號</span>
          <input class="content" disabled value="" name="ven_id">
      </div>
      
      <div class="item">
          <span class="title">認證狀態</span>
          <input class="content" disabled value="" name="ven_id_qu">
      </div>

      <div class="item">
          <span class="title">負責人</span>
          <input class="content" disabled value="" name="ven_name" required maxlength="3"> 
      </div>

      <div class="item">
          <span class="title">聯絡電話</span>
          <input class="content" disabled value="" name="ven_tel" type="tel" size="10" required>
      </div>
      <div class="item rwd">
          <span class="title">Email</span>
          <input class="content" disabled value="" name="ven_email" type="email" required>
      </div>
      <div class="btn">
          <input type="button" value="修改資料" name="edit" id="edit" class="btn-cir_gr2 fw_6">
          <input type="button" value="確認送出" name="submit" id="submit" class="btn-cir_pk2 fw_6">
      </div>
    </form>
</div>
```
{% endtab %}

{% tab title="js" %}
```php
var itsclose = true;
function doFirst(){
  //非同步畫面呈現（綁資料庫）
  function loadVMfoData(){
    let xhr = new XMLHttpRequest();
    let url = "./connect/vendor_member_fromUT_start.php";
    // let jdata = JSON.stringify(data);
    xhr.onload = function(){
      if(xhr.status == 200){
        let jresult = JSON.parse(xhr.responseText);
        switch(jresult.vq){
          case '0':
            $('#class1 [name="ven_id_qu"]').val('待認證')
            break;
          case '1':
            $('#class1 [name="ven_id_qu"]').val('認證未通過')
            break;
          case '2':
            $('#class1 [name="ven_id_qu"]').val('認證已通過')
            break;
        }
        $('#class1 [name="ven_no"]').val(jresult.vno)
        $('#class1 [name="ven_id"]').val(jresult.vi)
        $('#class1 [name="ven_name"]').val(jresult.vn)
        $('#class1 [name="ven_tel"]').val(jresult.vt)
        $('#class1 [name="ven_email"]').val(jresult.ve)
      }else{
        alert(xhr.status)
      }
    }
    xhr.open("GET",url,true);
    xhr.send(null);
  }
  loadVMfoData();
  sendInData();
  //非同步傳送資料
  function changeVMfoData(){
    let xhr = new XMLHttpRequest();
    let url = "./connect/vendor_member_fromUT.php";
    let jdata = JSON.stringify(data);
    xhr.onload = function(){
      if(xhr.status == 200){
        let jresult = JSON.parse(xhr.responseText);
        // console.log(jresult)
        $('#class1 [name="ven_name"]').val(jresult.vn)
        $('#class1 [name="ven_tel"]').val(jresult.vt)
        $('#class1 [name="ven_email"]').val(jresult.ve)
      }else{
        alert(xhr.status)
      }
    }
    xhr.open("POST",url,true);
    xhr.setRequestHeader("content-type","application/json")
    xhr.send(jdata);
  } 
  
  //修改資料按鈕
  $('#class1 #edit').click(function(){
    let reqElm = document.querySelectorAll('#class1 [required]')
    for(let i=0;i<reqElm.length;i++){
      itsclose = false;
      reqElm[i].disabled = false;
    }
  })
  
  //事件聆聽
  document.querySelector('#class1 [name="ven_name"]').addEventListener('change',sendInData)
  document.querySelector('#class1 [name="ven_tel"]').addEventListener('change',sendInData)
  document.querySelector('#class1 [name="ven_email"]').addEventListener('change',sendInData)
  document.querySelector('#class1 #submit').addEventListener('click',function(e){
    var valid = this.form.checkValidity();
    if(valid){
      e.preventDefault();
      if(itsclose==false){
        changeVMfoData()
        let reqElm = document.querySelectorAll('#class1 [required]')
        for(let i=0;i<reqElm.length;i++){
          itsclose = true;
          reqElm[i].disabled = true;
        }
      }
    }else{
      // alert('格式不對或欄位未填')
      document.querySelector('#class1 [name="ven_email"]').reportValidity()
      document.querySelector('#class1 [name="ven_tel"]').reportValidity()
      document.querySelector('#class1 [name="ven_name"]').reportValidity()
    }
  })
}//doFirst()
//資料裡面放東西
function sendInData(){
  data = {}
  let ven_nameVal = document.querySelector('#class1 [name="ven_name"]').value
  let ven_telVal = document.querySelector('#class1 [name="ven_tel"]').value
  let ven_emailVal = document.querySelector('#class1 [name="ven_email"]').value
  data.vn = ven_nameVal;  //送PHP記得這個物件的索引值名稱唷~~
  data.vt = ven_telVal;   //送PHP記得這個物件的索引值名稱唷~~
  data.ve = ven_emailVal; //送PHP記得這個物件的索引值名稱唷~~
}
window.addEventListener('load',doFirst);
```
{% endtab %}

{% tab title="PHP\(connect\)" %}
```php
<?php
//連線(連資料庫帳號密碼等設定)用的
  $dsn = 'mysql:host=localhost;port=3306;dbname=yesman;charset=utf8';
  $user = '資料庫帳號';
  $password = '資料庫密碼';
  $options  = array(PDO::ATTR_CASE=>PDO::CASE_NATURAL, 
                    PDO::ATTR_ERRMODE=>PDO::ERRMODE_EXCEPTION);
  $pdo = new PDO($dsn,$user,$password,$options);
?>
```
{% endtab %}

{% tab title="PHP\(load\)" %}
```php
<?php
//當畫面跑完，要撈資料庫的資料到畫面上
//./connect/vendor_member_fromUT_start.php
$venNo = 6;//測試用，寫死的
try{
  require_once('./connect.php');
  $sql = 'select * from vendor_info where ven_no=:venNo;';
  $veninfoU = $pdo->prepare($sql);
  $veninfoU->bindValue(':venNo',$venNo);
  $veninfoU->execute();
  while($veninfoURow=$veninfoU->fetchObject()){
    $jresult = array(
      'vno'=>$veninfoURow->ven_no,
      'vi'=>$veninfoURow->ven_id,
      'vq'=>$veninfoURow->ven_id_qu,
      'vn'=>$veninfoURow->ven_name,
      'vt'=>$veninfoURow->ven_tel,
      've'=>$veninfoURow->ven_email
    );
  }
  echo json_encode($jresult);
}catch(PDOException $e){
  echo "錯誤 : ".$e -> getMessage()."<br>";
  echo "行號 : ".$e -> getLine()."<br>";
}
?>
```
{% endtab %}

{% tab title="PHP\(sendNback\)" %}
```php
<?php
//當按下送出鍵，資料傳給資料庫、並讓畫面資料呈現剛剛輸入的(這好像..)..
//./connect/vendor_member_fromUT.php
$venNo = 6;//測試用，寫死的
$jdata = json_decode(file_get_contents('php://input'), true);
// $jresult = array(23=>'234',347=>'三三娘娘');
$vname  = $jdata["vn"];//JS那邊命名的物件名稱
$vtel   = $jdata["vt"];//JS那邊命名的物件名稱
$vemail = $jdata["ve"];//JS那邊命名的物件名稱
try{
  require_once('./connect.php');
  $sql = 'update vendor_info
          set ven_name=:vname,ven_tel=:vtel,ven_email=:vemail
          where ven_no=:venNo;';
  $sql2 = 'select * from vendor_info where ven_no=:venNo;';
  $veninfoU = $pdo->prepare($sql);
  $veninfoU->bindValue(':vname',$vname);
  $veninfoU->bindValue(':vtel',$vtel);
  $veninfoU->bindValue(':vemail',$vemail);
  $veninfoU->bindValue(':venNo',$venNo);
  $veninfoU->execute();
  $veninfoU = $pdo->prepare($sql2);
  $veninfoU->bindValue(':venNo',$venNo);
  $veninfoU->execute();
  while($veninfoURow=$veninfoU->fetchObject()){
    $jresult = array(
      'vn'=>$veninfoURow->ven_name,
      'vt'=>$veninfoURow->ven_tel,
      've'=>$veninfoURow->ven_email
    );
  }
  echo json_encode($jresult);
}catch(PDOException $e){
  echo "錯誤 : ".$e -> getMessage()."<br>";
  echo "行號 : ".$e -> getLine()."<br>";
}
?>
```
{% endtab %}
{% endtabs %}



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

