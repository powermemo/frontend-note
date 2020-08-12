---
description: 一種資料交換的格式，可以是副檔名
---

# JSON

## HTML的JSON

{% hint style="info" %}
兩種常見的方法

* `JSON.stringify(js物件) //物件|陣列轉字串(JSON)`
* `JSON.parse(json字串)   //字串(JSON)轉物件|陣列`
{% endhint %}

對應範例檔0804「json.html」

{% tabs %}
{% tab title="stringify" %}
JSON.stringify\(js物件\) //物件轉字串

```javascript
 var emp={
  empno: "7001",
  ename: "Andy",
  sal: 33000,
  phone:["03-4257387","03-168168","0933168168"]
}
var str = JSON.stringify(emp);     //🟡
document.write("json:",str,"<br>");
//【result】json:{"empno":"7001","ename":"Andy","sal":33000,"phone":["03-4257387","03-168168","0933168168"]}
```

```javascript
var emp={
    empno: "7001",
    ename: "Andy",
    sal: 33000,
    phone:{
        O:"03-4257387",
        H:"03-168168",
        M:"0933168168",
    },
}
var str = JSON.stringify(emp);     //🟡
document.write("json:",str,"<br>");
//【result】json:{"empno":"7001","ename":"Andy","sal":33000,"phone":{"O":"03-4257387","H":"03-168168","M":"0933168168"}}
```
{% endtab %}

{% tab title="parse" %}
JSON.parse\(json字串\)//字串轉物件

```javascript
var str = '{"empno": "7001","ename": "Andy","sal": "33000","phone":["03-4257387","03-168168","0933168168"]}';
var obj = JSON.parse(str);                    //🟡
document.write("obj.empno:",obj.empno,"<br>");
document.write("obj.ename:",obj.ename,"<br>");
document.write("obj.sal:",obj.sal,"<br>");
document.write("obj.phone:",obj.phone,"<br>");//array 會 toString
for(let i in obj.phone){
    document.write(`obj.phone[${i}]: ${obj.phone[i]}<br>`);
}
// 【result】obj.empno:7001
// 【result】obj.ename:Andy
// 【result】obj.sal:33000
// 【result】obj.phone:03-4257387,03-168168,0933168168 //array 會 toString
// 【result】obj.phone[0]: 03-4257387"
// 【result】obj.phone[1]: 03-168168"
// 【result】obj.phone[2]: 0933168168"

```

```javascript
 var str = '{"empno": "7001","ename": "Andy","sal": "33000","phone":{"O":"03-4257387","H":"03-168168","M":"0933168168"}}';
 var obj = JSON.parse(str);
 document.write("obj.empno:",obj.empno,"<br>");      //7001
 document.write("obj.ename:",obj.ename,"<br>");      //Andy
 document.write("obj.sal:",obj.sal,"<br>");          //33000
 document.write("obj.phone:",obj.phone,"<br>");      //[object Object]
 document.write("obj.phone.H:",obj.phone.H,"<br>");  //03-168168
 document.write("obj.phone.M:",obj.phone.M,"<br>");  //0933168168
 // 【result】obj.empno:7001
 // 【result】obj.ename:Andy
 // 【result】obj.sal:33000
 // 【result】obj.phone:[object Object]               //[object Object]
 // 【result】obj.phone.H:03-168168
 // 【result】obj.phone.M:0933168168
```
{% endtab %}
{% endtabs %}

## PHP的JSON

{% hint style="info" %}
* `json_encode()  //陣列|物件   轉   字串`
* `json_decode()  //字串        轉   陣列|物件`
{% endhint %}

對應範例檔0804「json.php」

{% tabs %}
{% tab title="json\_encode" %}
json\_encode\(\)  //陣列\|物件   轉   字串

```php
//PHP的索引陣列轉成json
$arr = array(11,22,33);
$str = json_encode($arr);
echo "json: $str <br>";
//【result】json: [11,22,33]
```

```php
//PHP的associative陣列
$empRow = array("empno"=>"7003","ename"=>"Ann","sal"=>33000);
$str = json_encode($empRow);
echo "json:$str<br>";
//【result】json:{"empno":"7003","ename":"Ann","sal":33000}
```
{% endtab %}

{% tab title="json\_decode" %}
json\_decode\(\)  //字串        轉   陣列\|物件

```php
//json格式一：轉成PHP的陣列
$str = '[11,22,33]';
$arr2 = json_decode($str);
// echo "arr2[1] : {$arr2[1]} <br>";
foreach($arr2 as $i =>$data){
    echo "$i : $data <br>";
}
// 【result】0 : 11
// 【result】1 : 22
// 【result】2 : 33
```

```php
//json格式二：轉成PHP的associative陣列
$str = '{"empno":"7001","ename":"Ann","sal":33000}';
$arr3 = json_decode($str,true);//第二個參數表示是否轉乘associative陣列
// foreach($arr3 as $i =>$data){
//     echo "$i : $data <br>";
// }
echo $arr3["empno"], "<br>";
echo $arr3["ename"], "<br>";
echo $arr3["sal"], "<br>";
// 【result】7001
// 【result】Ann
// 【result】33000
```

```php
//json格式二：轉成PHP的物件
//在JS的「.」；在PHP的「->」
$str = '{"empno":"7001","ename":"Ann","sal":33000}';
//下面第二個參數沒給，就是「物件」false
$obj = json_decode($str,false);//第二個參數表示是否轉乘associative陣列，false表示轉成物件
echo $obj->empno, "<br>";
echo $obj->ename, "<br>";
echo $obj->sal, "<br>";
// 【result】7001
// 【result】Ann
// 【result】33000
```
{% endtab %}
{% endtabs %}

## 🍵應用－串聯多頁面會員登入

參照資料夾「login\_navBar」

{% tabs %}
{% tab title="index+navBar" %}
「index.php」首頁  
連結「navBar.inc」，登入區域分離  
連結「login.js」，登入控制

```php
//index.php
<html>
<head>
<meta charset="utf-8">
<title>董董購物網</title>
<link rel="stylesheet" type="text/css" href="jsLogin.css">
<link rel="icon" href="大頭照.jpg">
</head>

<body>
<!---------------------這是navbar-------------------------->  
<?php 
require_once("navBar.inc");
?>
<!---------------------這是navbar-------------------------->


<div id="content">
<center><h1>這是首頁</h1></center><br>
<p><center><a href="about.php">關於我們</a></center></p>
<p><center><a href="discuss.php">討論區</a></center></p>
</div>

<div id="footer"></div>

</div>
<script src="login.js">
</script>
</body>
</html>
```

```php
//navBar.inc
<!-- 燈箱：登入 -->
<div id="lightBox" style="display:none">
<table border="1" align="center" cellspacing="0" id="tableLogin">
<tr><td>帳號</td><td><input type="text" name="memId" id="memId"></td></tr>
<tr><td>密碼</td><td><input type="password" name="memPsw" id="memPsw"></td></tr>
<tr><td colspan="2" align="center">
        <input type="button" id="btnLogin" value="登入">
        <input type="button" id="btnLoginCancel" value="取消">
    </td></tr>
</table>
</div>

<!-- wrapper -->
<div id="wrapper">
<!-- 登入bar -->
<img src="大頭照.jpg">
<div id="bar" style="position: absolute;top:0;right: 20px">
<span id="memName">&nbsp;</span>   <!-- 使用者姓名 -->
<span id="spanLogin">登入</span>
</div>
```
{% endtab %}

{% tab title="jsLogin" %}
「login.js」，登入控制  
連結「logout.php」，關閉session資料  
連結「ajaxLogin.php」，將資料寫入session  
連結「getLonginInfo.php」

```javascript
//login.js
let member;

function $id(id){
  return document.getElementById(id);
} 

function showLoginForm(){
  //檢查登入bar面版上 spanLogin 的字是登入或登出
  //如果是登入，就顯示登入用的燈箱(lightBox)
  //如果是登出
  //將登入bar面版上，登入者資料清空 
  //spanLogin的字改成登入
  //將頁面上的使用者資料清掉
  if($id('spanLogin').innerHTML == "登入"){
    $id('lightBox').style.display = 'block'; //show 燈箱
  }else{ //登出
    
    //-----------------------------回Server端做登出
    let xhr = new XMLHttpRequest();
    xhr.onload = function(){
      if(xhr.status == 200){
        $id('memName').innerHTML = '&nbsp';
        $id('spanLogin').innerHTML = '登入';       
      }else{
        alert(xhr.status);
      }

    }
    xhr.open("get", "logout.php", true);
    xhr.send(null);
  }

}//showLoginForm

function sendForm(){
  //=====================使用Ajax 回server端,取回登入者姓名, 放到頁面上  
  let xhr = new XMLHttpRequest();

  xhr.onload = function(){
    if(xhr.status == 200){
        member = JSON.parse(xhr.responseText);
        if(member.memId === undefined){
          alert("帳密錯誤");
        }else{ //登入成功
          $id("memName").innerText = member.memName;
          $id("spanLogin").innerText = "登出";  
           //將登入表單上的資料清空，並隱藏起來
          $id('lightBox').style.display = 'none';
          $id('memId').value = '';
          $id('memPsw').value = '';      
        }

    }else{
      alert(xhr.status);
    }
  }

  xhr.open("post", "ajaxLogin.php", true);
  xhr.setRequestHeader("content-type", "application/x-www-form-urlencoded");
  let data_info = `memId=${$id("memId").value}&memPsw=${$id("memPsw").value}`;
  xhr.send(data_info);
  
}

function cancelLogin(){
  //將登入表單上的資料清空，並將燈箱隱藏起來
  $id('lightBox').style.display = 'none';
  $id('memId').value = '';
  $id('memPsw').value = '';
}


function getLoginInfo(){
  let xhr = new XMLHttpRequest();

  xhr.onload = function(){
    member = JSON.parse(xhr.responseText);
    if(member.memId){ 
      $id("memName").innerText = member.memName;
      $id("spanLogin").innerText = "登出";
    }
  }

  xhr.open("get", "getLoginInfo.php", true);
  xhr.send(null);
}

function init(){
    //-----------------------回Server端取回登入者的資訊
  getLoginInfo();
  //===設定spanLogin.onclick 事件處理程序是 showLoginForm

  $id('spanLogin').onclick = showLoginForm;

  //===設定btnLogin.onclick 事件處理程序是 sendForm
  $id('btnLogin').onclick = sendForm;

  //===設定btnLoginCancel.onclick 事件處理程序是 cancelLogin
  $id('btnLoginCancel').onclick = cancelLogin;

}; //window.onload

window.addEventListener("load", init, false);

```
{% endtab %}

{% tab title="longin" %}
「logout.php」，關閉session資料  
「ajaxLogin.php」，將資料寫入session  
「getLonginInfo.php」

```text
//logout.php
<?php 
session_start();
session_unset();
 ?>
```

```php
//ajaxLogin.php
<?php
session_start();
try{
  require_once("../../connectBooks.php");
  $sql = "select * from `member` where memId=:memId and memPsw=:memPsw"; 
  $member = $pdo->prepare($sql);
  $member->bindValue(":memId", $_POST["memId"]);
  $member->bindValue(":memPsw", $_POST["memPsw"]);
  $member->execute();

  if( $member->rowCount()==0){ //查無此人
	  echo "{}";
  }else{ //登入成功
    //自資料庫中取回資料
  	$memRow = $member->fetch(PDO::FETCH_ASSOC);

  	//將登入者的資料先寫入session
  	$_SESSION["memNo"] = $memRow["no"];
  	$_SESSION["memId"] = $memRow["memId"];
  	$_SESSION["memName"] = $memRow["memName"];
  	$_SESSION["tel"] = $memRow["tel"];
  	$_SESSION["email"] = $memRow["email"];

    //送出登入者的姓名資料
    $result = array("memId"=>$memRow["memId"], "memName"=>$memRow["memName"],"email"=>$memRow["email"]);
    echo json_encode($result);
  }
}catch(PDOException $e){
  echo $e->getMessage();
}
?>


```

```php
//getLonginInfo.php
<?php 
session_start();
if( isset($_SESSION["memId"]) === true){
	//送出登入者的姓名資料
    $result = array("memId"=>$_SESSION["memId"], "memName"=>$_SESSION["memName"],"email"=>$_SESSION["email"]);
    echo json_encode($result);
}else{
	echo "{}";
}
?>
```
{% endtab %}
{% endtabs %}





