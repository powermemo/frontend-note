---
description: 一種非同步的技術，它不是新語言，它不能是副檔名
---

# Ajax

## 建立Ajax核心物件 - XMLHttpRequest

```aspnet
var xhr = newXMLHttpRequest();
```

### XMLHttpRequest methods方法

| 方法名稱                                 | 說明                                                    |
| ------------------------------------ | ----------------------------------------------------- |
| abort()                              | 停止當前請求                                                |
| getAllResponseHeaders()              | <p>取得HTTP的所有回應標頭</p><p>ex. &#x3C;meta charset...></p> |
| getResponseHeader("header")          | 取得某特定HTTP回應之標頭/字串值                                    |
| **open("method","url",async)**       | 開啟對伺服端的連結                                             |
| **send("content")**                  | 向伺服器發送請求，並將資料送到伺服器端                                   |
| **setRequestHeader("head","value")** | 設定HTTP請求的請求標頭。                                        |

#### open("_method_","_url_",_async_)

開啟對伺服端的連結

* method參數：如GET或POST
  * POST的使用時機
    * 不想用到cache中的檔案
    * 要傳送的資料太大
    * 安全性考量
* url參數：指定所要存取檔案的位置
* async參數：決定採用非同步傳輸或不採用
  * `true` 非同步  |   false 同步

#### send("_content_")

向伺服器發送請求，並將資料送到伺服器端。

* [send(null)](https://google.com)：open()的method為GET
* [send(data\_info)](https://google.com)：open()的method為POST
  * data\_info為自定義
  * 格式："欄名1=值**&**欄名2=值**&**..."

#### setRequestHeader(_header_,_value_)

method為POST時使用，設定HTTP請求的請求標頭。\
POST一定要設哦！

* header：Http的標頭名稱
* value：標頭名稱的值

```aspnet
xhr.setRequestHeader("content-Type","application/x-www-form-urlencoded")
```

### XMLHttpRequest attributes屬性

| 屬性名稱               | 說明                                                                                         |
| ------------------ | ------------------------------------------------------------------------------------------ |
| readyState         | <p>請求處理狀態</p><p>ex. 0→1→2...</p>                                                           |
| onreadystatechange | <p>請求的處理狀態改變時應執行的事件處器</p><p>ex.readyState狀態 0→1→2...</p>                                   |
| status             | <p>伺服器回傳的Http狀態碼</p><p>ex.<strong>404</strong>找不到檔案、<strong>500</strong>server端連線問題</p>    |
| statusText         | <p>伺服器回傳的Http狀態文字訊息</p><p>ex.404<strong>找不到檔案</strong>、500<strong>server端連線問題</strong></p> |
| responseText       | 伺服器的回傳資料，回應的內容為一個字串                                                                        |
| responseXML        | 伺服器的回傳資料，回應的內容為XML Document(串流文件檔案)                                                        |

{% hint style="info" %}
onload(發生在readyState=4之後)、\
timeout、\
ontimeout
{% endhint %}

### readyState屬性

記錄server端目前針對請求的處理狀態。

| 狀態 | 常數                | 說明                                            |
| -- | ----------------- | --------------------------------------------- |
| 0  | UNSENT            | 尚未初始化(request not initialized)                |
| 1  | OPENED            | 請求已被建立(server connection established)         |
| 2  | HEADERS\_RECEIVED | 請求已被送出(request received)                      |
| 3  | LOADING           | 請求正在處理(processing request)                    |
| 4  | DONE              | 請求已完成(request finished and response is ready) |

### status屬性

server端回應的Http狀態碼

* 主要三個層級，1st數字大類、2nd數字中類、3rd數字小類
  * 1xx參考資訊(Informational)
  * 2xx成功(OK)
  * 3xx重新導向(Redirection)
  * 4xx用戶端錯誤(Client Error)
  * 5xx伺服器錯誤(Server Error)

### 🍵範例－XMLHttpRequest

{% tabs %}
{% tab title="GET N POST" %}
* 「GetResponseText.html」「GetResponseText.php」
* 「PostResponseText.html」「PostResponseText.php」
* 檢查帳號是否重複

#### PHP的部分(如果你用$\_REQUEST\['']抓資料)不變。

```php
<?php
try{
  require_once("../connectBooks.php");
  $memId = $_POST["memId"];
  $sql = "select * from `member` where memId=:memId";
  $member = $pdo->prepare($sql);
  $member->bindValue(":memId", $memId);
  $member->execute();
  if( $member->rowCount() !=0){echo "此帳號已存在, 不可用";}
  else{ echo "此帳號可使用"; } 
}catch(PDOException $e){
  echo "error";
}
?>
```

#### HTML的JS五個步驟（第三第四會因post | get而有不同）

```javascript
function checkId(){  
//step1. 產生XMLHttpRequest物件
  let xhr = new XMLHttpRequest();
//step 2.註冊callback function 
  xhr.onload = function(){
    if(xhr.status == 200){alert(xhr.responseText)}
    else{alert(xhr.status)}
  }
//step 3.設定好所要連結的程式🟡【GET】
   let url = "0728GetResponseText.php?memId=" + document.getElementById("memId").value;
  xhr.open('get',url,true)
//step 4.送出資料          🟡【GET】
  xhr.send(null)
}
//..........................................
//step 5.與畫面產生連結
window.addEventListener("load", function(){
  document.getElementById("btnCheckId").addEventListener("click", checkId, false); }, false)
```

```javascript
function checkId(){  
//step1. 產生XMLHttpRequest物件
  let xhr = new XMLHttpRequest();
//step 2.註冊callback function 
  xhr.onload = function(){
    if(xhr.status == 200){alert(xhr.responseText)}
    else{alert(xhr.status)}
  }
//step 3.設定好所要連結的程式🟡【POST】
  let url = '0730PostResponseText.php'
  xhr.open('post',url,true)
//step 4.送出資料🟡【POST】
  let data_info = 'memId=' + document.querySelector('#memId').value
  xhr.setRequestHeader("content-type","application/x-www-form-urlencoded")
  xhr.send(data_info)
}
//..........................................
//step 5.與畫面產生連結
window.addEventListener("load", function(){
  document.getElementById("btnCheckId").addEventListener("click", checkId, false); }, false)
```
{% endtab %}

{% tab title="responseText" %}
對應範例檔案07/30「getMore.html」「getMore.php」\
取得會員資料（僅字串相連）

```aspnet
//getMore.html
<div>首頁>>會員專區</div>
<center>
會員帳號<input type="text" name="memId" id="memId"/>
<input type="button" value="取得會員資料" onclick="getMember()"/>
<div id="showPanel"></div>
</center>
<script>
function getMember(){
  var xhr = new XMLHttpRequest();
  xhr.onreadystatechange=function (){
      if( xhr.readyState == 4){
        if( xhr.status == 200 ){
          document.getElementById("showPanel").innerHTML = xhr.responseText;  
        }else{
          alert( xhr.status );
        }
      }
  }
  var url = "getMore.php?memId=" + document.getElementById("memId").value;
  xhr.open("Get", url, true);
  xhr.send( null );
}
</script>
```

```php
//getMore.php
<?php
try{
  require_once("../connectBooks.php");
  $sql = "select * from `member` where memId=:memId";
  $member = $pdo->prepare( $sql );
  $member->bindValue(":memId", $_REQUEST["memId"]);
  $member->execute();
  //如果找得資料,將會員資料送出
  if( $member->rowCount() == 0 ){
    echo "not found~";
  }else{
    $memRow = $member->fetch(PDO::FETCH_ASSOC);
  	$str="";
  	foreach( $memRow as $i => $data ){
  	  $str .= $data . "," ;
  	}
  	echo $str;
  }	
}catch(PDOException $e){
  echo $e->getMessage();
}
?>
```
{% endtab %}
{% endtabs %}

## XML

XML可以是副檔名。\
大概長這樣，就是比較嚴謹的編碼方式，我沒有要特別介紹..

```
<emp>
  <empno>7566</empno>
  <ename>JONES</ename>
  <job>MANAGER</job>
  <mgr>7839</mgr>
  <hiredate>1981-04-02</hiredate>
  <sal>2975</sal>
  <deptno>20</deptno>
</emp>
```

### W3C DOM 節點

![DOM](<../.gitbook/assets/image (43).png>)

| nodeType常數                    | nodeType值 | 說明               |
| ----------------------------- | --------- | ---------------- |
| ELEMENT\_NODE                 | 1         | 元素節點ex.div,h2... |
| ATTRIBUTE\_NODE               | 2         |                  |
| TEXT\_NODE                    | 3         | 文字節點             |
| CDATA\_SECTION\_NODE          | 4         |                  |
| ENTITY\_REFERENCE\_NODE       | 5         |                  |
| ENTITY\_NODE                  | 6         |                  |
| PROCESSING\_INSTRUCTION\_NODE | 7         |                  |
| COMMENT\_NODE                 | 8         |                  |
| DOCUMENT\_NODE                | 9         |                  |
| DOCUMENT\_TYPE\_NODE          | 10        |                  |
| DOCUMENT\_FRAGMENT\_NODE      | 11        |                  |
| NOTATION\_NODE                | 12        |                  |

範例

| node               | nodeType | nodeName | nodeValue          |
| ------------------ | -------- | -------- | ------------------ |
| div                | 1(元素節點)  | div      | undefined          |
| h2                 | 1(元素節點)  | h2       | undefined          |
| Welcome to W3C DOM | 3(文字節點)  | #text    | Welcome to W3C COM |

### W3C DOM 文件的methods

| 語法                                                                                                                            | 說明                      |
| ----------------------------------------------------------------------------------------------------------------------------- | ----------------------- |
| <p><code>document.createElement(</code><em><code>tagName</code></em><code>)</code></p><p>例如document.createElement("div")</p>  | **建立**一個標籤名稱為tagName的元素 |
| <p><code>document.createTextNode(</code><em><code>text</code></em><code>)</code></p><p>例如document.createTextNode("Hello")</p> | **建立**一個包含靜態文字的節點       |

### W3C DOM 節點的attribute

![](<../.gitbook/assets/image (44).png>)

| 屬性名稱            | 說明               |
| --------------- | ---------------- |
| childNodes      | 傳回目前元素所有子節點的節點清單 |
| firstChild      | 傳回目前元素的第一個子節點    |
| lastChild       | 傳回目前元素的最後一個子節點   |
| nextSibling     | 傳回緊鄰在目前節點之後的節點   |
| previousSibling | 傳回緊鄰在目前節點之前的節點   |
| parentNode      | 傳回元素的父節點         |
| nodeName        | 傳回節點的節點名稱        |
| nodeType        | 傳回節點的節點型態        |
| nodeValue       | 傳回節點的值           |

### W3C DOM 節點的methods

| 語法                                                                                         | 說明                                                |
| ------------------------------------------------------------------------------------------ | ------------------------------------------------- |
| <p><code>node.appendChild(childNode)</code></p><p>例如tr.appendChild(td)</p>                 | 將指定的子節點(childNode)加到node的子節點清單中                   |
| <p><code>node.insertBefore(aNode,bNode)</code></p><p>例如tr.insertBefore(newTd,targetTd)</p> | <p>將指定的節點(aNode)插到node之下，<br>特定節點(bNode)之前</p>    |
| <p><code>node.removeChild(childNode)</code></p><p>例如tr.removeChild(td)</p>                 | 將子節點(childNode)從node中刪除                           |
| <p><code>node.replaceChild(aNode,bNode)</code></p><p>例如re.replaceChild(aCell,bCell)</p>    | <p>將此node的子節點中，某特定節點(bNode)<br>換成另一個節點(aNode)</p> |
| <p><code>node.hasChildNodes()</code></p><p>例如tr.hasChildNodes()</p>                        | 傳回一個布林值，指出此node是否有子節點                             |

### W3C DOM 元素的methods

| 語法                                                                                      | 說明                                       |
| --------------------------------------------------------------------------------------- | ---------------------------------------- |
| <p>element.getAttribute(attributeName)</p><p>例如table.getAttribute("borderColor")</p>    | 取得element中某屬性(attributeName)的值           |
| <p>element.setAttribute(attributeName,value)</p><p>例如table.setAttribute("border",1)</p> | 設定element中某屬性(attributeName)的值           |
| <p>element.removeAttribute(attributeName)</p><p>例如table.removeAttibute("border")</p>    | 將指定的屬性(attributeName)從此element中移除        |
| <p>element.getElementsByTagName(tagName)</p><p>例如table.getElementsByTagName("td")</p>   | <p>取得此element內標籤名稱為tagName的<br>所有子元素</p> |

### 🍵範例－XML－動態建立表格

{% tabs %}
{% tab title="responseXML" %}
對應範例檔案07/30「getMore\_XML.html」「getMore\_XML.php」\
取得會員資料（XML標籤）

```aspnet
//getMore_XML.html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF-8">
    <title>測試</title>
    <style>
        .memTable th{
            background-color: pink;
        }
        .memTable td{
            border-bottom: 1px dotted deeppink;
        }
    </style>
</head>
<body>
<div>首頁>>會員專區</div>
<center>
    <div>
        <label for="memId">會員帳號</label>
        <input type="text" name="memId" id="memId"/>
        <input type="button" value="取得會員資料" onclick="getMember()"/>
        <div id="showPanel"></div>
    </div>
</center>
<script>
    //「xmlDoc」這是從後端抓取的文件
    function showMember(xmlDoc){
        var table,tr,th,td,text,textNode;
        let fields = xmlDoc.documentElement.childNodes;
        table = document.createElement('table');
        for(let i=0;i<fields.length;i++){
            tr=document.createElement('tr');
            th=document.createElement('th');
            td=document.createElement('td');
            textNode=document.createTextNode(fields[i].nodeName);
            //因為只有一個孩子，以下「firstChild」同等「lastChilde」/「childNodes[0]」
            text=document.createTextNode(fields[i].firstChild.nodeValue);
            table.appendChild(tr);
            tr.appendChild(th);
            th.appendChild(textNode);
            tr.appendChild(td);
            td.appendChild(text);
        }
        document.querySelector('#showPanel').appendChild(table);
        table.setAttribute("class","memTable");
    }
    function getMember(){
        var xhr = new XMLHttpRequest();
        xhr.onload=function(){
            if(xhr.status ==200){
                showMember(xhr.responseXML);
            }else{
                alert(xhr.status);
            }
        }
        var url = "0731TESTgetMore.php?memId=" + document.querySelector('#memId').value;
        xhr.open("Get", url, true);
        xhr.send( null );
    }
</script>
</body>
</html>
```

```php
//getMore_XML.php
<?php
try{
  require_once("../connectBooks.php");
  $sql = "select * from `member` where memId=:memId";
  $member = $pdo->prepare($sql);
  $member->bindValue(":memId", $_GET["memId"]);
  // $member->bindValue(":memId", "Sara");
  $member->execute();

  //如果找得資料，取回資料，送出xml文件
  if($member->rowCount() == 0){ //無此會員資料
  	echo "notFound";
  }else{
    $memRow = $member -> fetch(PDO::FETCH_ASSOC);
    $xml = '<?xml version="1.0" ?>';
    $xml .=  "<member>";
    $xml .=  "<memId>{$memRow["memId"]}</memId>";
    $xml .=  "<memName>{$memRow["memName"]}</memName>";
    $xml .=  "<tel>{$memRow["tel"]}</tel>";
    $xml .=  "<email>{$memRow["email"]}</email>";
    $xml .=  "</member>";
    header("content-type:text/xml");
    echo $xml;
  }
  
}catch(PDOException $e){
  echo $e->getMessage();
}
?>
```
{% endtab %}
{% endtabs %}

## JSON

一種資料交換的格式，可以是副檔名

### HTML的JSON

{% hint style="info" %}
兩種常見的方法

* `JSON.stringify(js物件) //物件|陣列轉字串(JSON)`
* `JSON.parse(json字串)   //字串(JSON)轉物件|陣列`
{% endhint %}

對應範例檔0804「json.html」

{% tabs %}
{% tab title="stringify" %}
JSON.stringify(js物件) //JS物件轉JSON字串

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
JSON.parse(json字串)//JSON字串轉JS物件

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

### PHP的JSON

{% hint style="info" %}
* `json_encode()  //陣列|物件   轉   字串`
* ``[`json_decode`](https://sites.google.com/site/phplearnmark/php/php-zhi-ling-qing-dan/json-han-shu/php-json\_decode)`()  //字串        轉   陣列|物件`
{% endhint %}

對應範例檔0804「json.php」

{% tabs %}
{% tab title="json_encode" %}
json\_encode()  //陣列|物件   轉   字串

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

{% tab title="json_decode" %}
json\_decode()  //字串        轉   陣列|物件

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
//🟡下面第二個參數沒給，就是「物件」false
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

##

### 🍵範例－JSON－串聯多頁面會員登入

參照資料夾「login\_navBar」

{% tabs %}
{% tab title="index+navBar" %}
「index.php」首頁\
連結「navBar.inc」，登入區域分離\
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
「login.js」，登入控制\
連結「logout.php」，關閉session資料\
連結「ajaxLogin.php」，將資料寫入session\
連結「getLonginInfo.php」

```javascript
//login.js
let member;

function $id(id){
  return document.getElementById(id);
} 

function showLoginForm(){
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
「logout.php」，關閉session資料\
「ajaxLogin.php」，將資料寫入session\
「getLonginInfo.php」

```
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

2
