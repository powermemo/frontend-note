---
description: 一種非同步的技術，它不是新語言，它不能是副檔名
---

# Ajax

## 建立Ajax核心物件 - XMLHttpRequest

```aspnet
var xhr = newXMLHttpRequest();
```

## XMLHttpRequest methods方法

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x65B9;&#x6CD5;&#x540D;&#x7A31;</th>
      <th style="text-align:left">&#x8AAA;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">abort()</td>
      <td style="text-align:left">&#x505C;&#x6B62;&#x7576;&#x524D;&#x8ACB;&#x6C42;</td>
    </tr>
    <tr>
      <td style="text-align:left">getAllResponseHeaders()</td>
      <td style="text-align:left">
        <p>&#x53D6;&#x5F97;HTTP&#x7684;&#x6240;&#x6709;&#x56DE;&#x61C9;&#x6A19;&#x982D;</p>
        <p>ex. &lt;meta charset...&gt;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">getResponseHeader(&quot;header&quot;)</td>
      <td style="text-align:left">&#x53D6;&#x5F97;&#x67D0;&#x7279;&#x5B9A;HTTP&#x56DE;&#x61C9;&#x4E4B;&#x6A19;&#x982D;/&#x5B57;&#x4E32;&#x503C;</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>open(&quot;method&quot;,&quot;url&quot;,async)</b>
      </td>
      <td style="text-align:left">&#x958B;&#x555F;&#x5C0D;&#x4F3A;&#x670D;&#x7AEF;&#x7684;&#x9023;&#x7D50;</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>send(&quot;content&quot;)</b>
      </td>
      <td style="text-align:left">&#x5411;&#x4F3A;&#x670D;&#x5668;&#x767C;&#x9001;&#x8ACB;&#x6C42;&#xFF0C;&#x4E26;&#x5C07;&#x8CC7;&#x6599;&#x9001;&#x5230;&#x4F3A;&#x670D;&#x5668;&#x7AEF;</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>setRequestHeader(&quot;head&quot;,&quot;value&quot;)</b>
      </td>
      <td style="text-align:left">&#x8A2D;&#x5B9A;HTTP&#x8ACB;&#x6C42;&#x7684;&#x8ACB;&#x6C42;&#x6A19;&#x982D;&#x3002;</td>
    </tr>
  </tbody>
</table>

### open\("_method_","_url_",_async_\)

開啟對伺服端的連結

* method參數：如GET或POST
  * POST的使用時機
    * 不想用到cache中的檔案
    * 要傳送的資料太大
    * 安全性考量
* url參數：指定所要存取檔案的位置
* async參數：決定採用非同步傳輸或不採用
  * `true` 非同步  \|   false 同步

### send\("_content_"\)

向伺服器發送請求，並將資料送到伺服器端。

* send\(null\)：open\(\)的method為GET
* send\(data\_info\)：open\(\)的method為POST
  * data\_info為自定義
  * 格式："欄名1=值**&**欄名2=值**&**..."

### setRequestHeader\(_header_,_value_\)

method為POST時使用，設定HTTP請求的請求標頭。  
POST一定要設哦！

* header：Http的標頭名稱
* value：標頭名稱的值

```aspnet
xhr.setRequestHeader("content-Type","application/x-www-form-urlencoded")
```

## XMLHttpRequest attributes屬性

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x5C6C;&#x6027;&#x540D;&#x7A31;</th>
      <th style="text-align:left">&#x8AAA;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">readyState</td>
      <td style="text-align:left">
        <p>&#x8ACB;&#x6C42;&#x8655;&#x7406;&#x72C0;&#x614B;</p>
        <p>ex. 0&#x2192;1&#x2192;2...</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">onreadystatechange</td>
      <td style="text-align:left">
        <p>&#x8ACB;&#x6C42;&#x7684;&#x8655;&#x7406;&#x72C0;&#x614B;&#x6539;&#x8B8A;&#x6642;&#x61C9;&#x57F7;&#x884C;&#x7684;&#x4E8B;&#x4EF6;&#x8655;&#x5668;</p>
        <p>ex.readyState&#x72C0;&#x614B; 0&#x2192;1&#x2192;2...</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">status</td>
      <td style="text-align:left">
        <p>&#x4F3A;&#x670D;&#x5668;&#x56DE;&#x50B3;&#x7684;Http&#x72C0;&#x614B;&#x78BC;</p>
        <p>ex.<b>404</b>&#x627E;&#x4E0D;&#x5230;&#x6A94;&#x6848;&#x3001;<b>500</b>server&#x7AEF;&#x9023;&#x7DDA;&#x554F;&#x984C;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">statusText</td>
      <td style="text-align:left">
        <p>&#x4F3A;&#x670D;&#x5668;&#x56DE;&#x50B3;&#x7684;Http&#x72C0;&#x614B;&#x6587;&#x5B57;&#x8A0A;&#x606F;</p>
        <p>ex.404<b>&#x627E;&#x4E0D;&#x5230;&#x6A94;&#x6848;</b>&#x3001;500<b>server&#x7AEF;&#x9023;&#x7DDA;&#x554F;&#x984C;</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">responseText</td>
      <td style="text-align:left">&#x4F3A;&#x670D;&#x5668;&#x7684;&#x56DE;&#x50B3;&#x8CC7;&#x6599;&#xFF0C;&#x56DE;&#x61C9;&#x7684;&#x5167;&#x5BB9;&#x70BA;&#x4E00;&#x500B;&#x5B57;&#x4E32;</td>
    </tr>
    <tr>
      <td style="text-align:left">responseXML</td>
      <td style="text-align:left">&#x4F3A;&#x670D;&#x5668;&#x7684;&#x56DE;&#x50B3;&#x8CC7;&#x6599;&#xFF0C;&#x56DE;&#x61C9;&#x7684;&#x5167;&#x5BB9;&#x70BA;XML
        Document(&#x4E32;&#x6D41;&#x6587;&#x4EF6;&#x6A94;&#x6848;)</td>
    </tr>
  </tbody>
</table>

{% hint style="info" %}
onload\(發生在readyState=4之後\)、  
timeout、  
ontimeout
{% endhint %}

### readyState屬性

記錄server端目前針對請求的處理狀態。

| 狀態 | 常數 | 說明 |
| :--- | :--- | :--- |
| 0 | UNSENT | 尚未初始化\(request not initialized\) |
| 1 | OPENED | 請求已被建立\(server connection established\) |
| 2 | HEADERS\_RECEIVED | 請求已被送出\(request received\) |
| 3 | LOADING | 請求正在處理\(processing request\) |
| 4 | DONE | 請求已完成\(request finished and response is ready\) |

### status屬性

server端回應的Http狀態碼

* 主要三個層級，1st數字大類、2nd數字中類、3rd數字小類
  * 1xx參考資訊\(Informational\)
  * 2xx成功\(OK\)
  * 3xx重新導向\(Redirection\)
  * 4xx用戶端錯誤\(Client Error\)
  * 5xx伺服器錯誤\(Server Error\)

## 🍵XMLHttpRequest範例

{% tabs %}
{% tab title="GET" %}
對應範例檔案07/28「GetResponseText.html」「GetResponseText.php」  
檢查帳號是否重複

```javascript
//..html的表單code部分沒有列出
//GetResponseText.html
function checkId(){  
  var xhr = new XMLHttpRequest();        //產生XMLHttpRequest物件
  //註冊callback function
  xhr.onreadystatechange = function(){    //狀態改變
    if(xhr.readyState == 4){             //server端已處理完畢
      if(xhr.status == 200){             //success
        alert(xhr.responseText);
      }else{
        alert(xhr.status);               //失敗時告訴我狀態碼是甚麼
      }
    }
  }

  //設定好所要連結的程式
  let url = "0728GetResponseText.php?memId=" + document.querySelector("#memId").value;
  xhr.open("get",url, true);          //xhr.readyStae--->1
  //送出資料
  xhr.send(null);                     //xhr.readyStae)--->2
}//function_checkId 

//..........................................
window.addEventListener("load", function(){
  // document.getElementById("btnCheckId").addEventListener("click", checkId, false);
  document.getElementById("memId").addEventListener("change", checkId, false);
}, false);
```

```php
//GetResponseText.php
<?php
try{
  require_once("../connectBooks.php");
  $memId = $_GET["memId"];              //取得前端送來的資料
  $sql = "select * from `member` where memId=:memId";
  $member = $pdo->prepare($sql);
  $member->bindValue(":memId",$memId);
  $member->execute();

  if( $member->rowCount() !=0){         //此帳號已存在, 不可用
    echo "此帳號已存在, 不可用";
  }else{ //此帳號可使用
    echo "此帳號可使用";
  } 
}catch(PDOException $e){
  echo "error";
}
?>
```
{% endtab %}

{% tab title="POST" %}
對應範例檔案07/30「PostResponseText.html」「PostResponseText.php」  
檢查帳號是否重複

```javascript
xhr.onload=function(){
    if(xhr.status == 200){
          alert(xhr.responseText);
        }else{
          alert(xhr.status);
        }
  }
  //設定好所要連結的程式
  let url = "0730PostResponseText.php";
  xhr.open("post",url,true);

  //送出資料
  let data_info = "memId=" + document.querySelector("#memId").value
  xhr.setRequestHeader("content-type","application/x-ww-form-urlencoded")
  xhr.send(data_info);
}//function_checkId 


//..........................................
window.addEventListener("load", function(){
  document.getElementById("btnCheckId").addEventListener("click", checkId, false);
}, false)
```

```php
<?php
try{
  require_once("../connectBooks.php");
  $memId = $_POST["memId"];              //取得前端送來的資料
  // $memId = "fghfhg";              //取得前端送來的資料
  $sql = "select * from `member` where memId=:memId";
  $member = $pdo->prepare($sql);
  $member->bindValue(":memId",$memId);
  $member->execute();

  if( $member->rowCount() !=0){         //此帳號已存在, 不可用
    echo "此帳號已存在, 不可用";
  }else{ //此帳號可使用
    echo "此帳號可使用";
  } 
}catch(PDOException $e){
  echo "error";
}
?>
```
{% endtab %}

{% tab title="responseText" %}
對應範例檔案07/30「getMore.html」「getMore.php」  
取得會員資料（僅字串相連）

```aspnet
//getMore.html
div>首頁>>會員專區</div>
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

{% tab title="responseXML" %}
對應範例檔案07/30「getMore.html」「getMore.php」  
取得會員資料（僅字串相連）

```aspnet
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
    function showMember(xmlDoc){
        var table,tr,th,td,text,textNode;
        let fields = xmlDoc.documentElement.childNodes;
        table = document.createElement('table');
        for(let i=0;i<fields.length;i++){
            tr=document.createElement('tr');
            th=document.createElement('th');
            td=document.createElement('td');
            textNode=document.createTextNode(fields[i].nodeName);
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
```

```php
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

## W3C DOM 節點

![DOM](../.gitbook/assets/image%20%2843%29.png)

| nodeType常數 | nodeType值 | 說明 |
| :--- | :--- | :--- |
| ELEMENT\_NODE | 1 | 元素節點ex.div,h2... |
| ATTRIBUTE\_NODE | 2 |  |
| TEXT\_NODE | 3 | 文字節點 |
| CDATA\_SECTION\_NODE | 4 |  |
| ENTITY\_REFERENCE\_NODE | 5 |  |
| ENTITY\_NODE | 6 |  |
| PROCESSING\_INSTRUCTION\_NODE | 7 |  |
| COMMENT\_NODE | 8 |  |
| DOCUMENT\_NODE | 9 |  |
| DOCUMENT\_TYPE\_NODE | 10 |  |
| DOCUMENT\_FRAGMENT\_NODE | 11 |  |
| NOTATION\_NODE | 12 |  |

範例

| node | nodeType | nodeName | nodeValue |
| :--- | :--- | :--- | :--- |
| div | 1\(元素節點\) | div | undefined |
| h2 | 1\(元素節點\) | h2 | undefined |
| Welcome to W3C DOM | 3\(文字節點\) | \#text | Welcome to W3C COM |

## W3C DOM 文件的methods

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x8A9E;&#x6CD5;</th>
      <th style="text-align:left">&#x8AAA;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p><code>document.createElement(</code><em><code>tagName</code></em><code>)</code>
        </p>
        <p>&#x4F8B;&#x5982;document.createElement(&quot;div&quot;)</p>
      </td>
      <td style="text-align:left"><b>&#x5EFA;&#x7ACB;</b>&#x4E00;&#x500B;&#x6A19;&#x7C64;&#x540D;&#x7A31;&#x70BA;tagName&#x7684;&#x5143;&#x7D20;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><code>document.createTextNode(</code><em><code>text</code></em><code>)</code>
        </p>
        <p>&#x4F8B;&#x5982;document.createTextNode(&quot;Hello&quot;)</p>
      </td>
      <td style="text-align:left"><b>&#x5EFA;&#x7ACB;</b>&#x4E00;&#x500B;&#x5305;&#x542B;&#x975C;&#x614B;&#x6587;&#x5B57;&#x7684;&#x7BC0;&#x9EDE;</td>
    </tr>
  </tbody>
</table>

## W3C DOM 節點的attribute

![](../.gitbook/assets/image%20%2844%29.png)

| 屬性名稱 | 說明 |
| :--- | :--- |
| childNodes | 傳回目前元素所有子節點的節點清單 |
| firstChild | 傳回目前元素的第一個子節點 |
| lastChild | 傳回目前元素的最後一個子節點 |
| nextSibling | 傳回緊鄰在目前節點之後的節點 |
| previousSibling | 傳回緊鄰在目前節點之前的節點 |
| parentNode | 傳回元素的父節點 |
| nodeName | 傳回節點的節點名稱 |
| nodeType | 傳回節點的節點型態 |
| nodeValue | 傳回節點的值 |

## W3C DOM 節點的methods

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x8A9E;&#x6CD5;</th>
      <th style="text-align:left">&#x8AAA;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p><code>node.appendChild(childNode)</code>
        </p>
        <p>&#x4F8B;&#x5982;tr.appendChild(td)</p>
      </td>
      <td style="text-align:left">&#x5C07;&#x6307;&#x5B9A;&#x7684;&#x5B50;&#x7BC0;&#x9EDE;(childNode)&#x52A0;&#x5230;node&#x7684;&#x5B50;&#x7BC0;&#x9EDE;&#x6E05;&#x55AE;&#x4E2D;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><code>node.insertBefore(aNode,bNode)</code>
        </p>
        <p>&#x4F8B;&#x5982;tr.insertBefore(newTd,targetTd)</p>
      </td>
      <td style="text-align:left">&#x5C07;&#x6307;&#x5B9A;&#x7684;&#x7BC0;&#x9EDE;(aNode)&#x63D2;&#x5230;node&#x4E4B;&#x4E0B;&#xFF0C;
        <br
        />&#x7279;&#x5B9A;&#x7BC0;&#x9EDE;(bNode)&#x4E4B;&#x524D;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><code>node.removeChild(childNode)</code>
        </p>
        <p>&#x4F8B;&#x5982;tr.removeChild(td)</p>
      </td>
      <td style="text-align:left">&#x5C07;&#x5B50;&#x7BC0;&#x9EDE;(childNode)&#x5F9E;node&#x4E2D;&#x522A;&#x9664;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><code>node.replaceChild(aNode,bNode)</code>
        </p>
        <p>&#x4F8B;&#x5982;re.replaceChild(aCell,bCell)</p>
      </td>
      <td style="text-align:left">&#x5C07;&#x6B64;node&#x7684;&#x5B50;&#x7BC0;&#x9EDE;&#x4E2D;&#xFF0C;&#x67D0;&#x7279;&#x5B9A;&#x7BC0;&#x9EDE;(bNode)
        <br
        />&#x63DB;&#x6210;&#x53E6;&#x4E00;&#x500B;&#x7BC0;&#x9EDE;(aNode)</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><code>node.hasChildNodes()</code>
        </p>
        <p>&#x4F8B;&#x5982;tr.hasChildNodes()</p>
      </td>
      <td style="text-align:left">&#x50B3;&#x56DE;&#x4E00;&#x500B;&#x5E03;&#x6797;&#x503C;&#xFF0C;&#x6307;&#x51FA;&#x6B64;node&#x662F;&#x5426;&#x6709;&#x5B50;&#x7BC0;&#x9EDE;</td>
    </tr>
  </tbody>
</table>

## W3C DOM 元素的methods

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x8A9E;&#x6CD5;</th>
      <th style="text-align:left">&#x8AAA;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>element.getAttribute(attributeName)</p>
        <p>&#x4F8B;&#x5982;table.getAttribute(&quot;borderColor&quot;)</p>
      </td>
      <td style="text-align:left">&#x53D6;&#x5F97;element&#x4E2D;&#x67D0;&#x5C6C;&#x6027;(attributeName)&#x7684;&#x503C;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>element.setAttribute(attributeName,value)</p>
        <p>&#x4F8B;&#x5982;table.setAttribute(&quot;border&quot;,1)</p>
      </td>
      <td style="text-align:left">&#x8A2D;&#x5B9A;element&#x4E2D;&#x67D0;&#x5C6C;&#x6027;(attributeName)&#x7684;&#x503C;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>element.removeAttribute(attributeName)</p>
        <p>&#x4F8B;&#x5982;table.removeAttibute(&quot;border&quot;)</p>
      </td>
      <td style="text-align:left">&#x5C07;&#x6307;&#x5B9A;&#x7684;&#x5C6C;&#x6027;(attributeName)&#x5F9E;&#x6B64;element&#x4E2D;&#x79FB;&#x9664;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>element.getElementsByTagName(tagName)</p>
        <p>&#x4F8B;&#x5982;table.getElementsByTagName(&quot;td&quot;)</p>
      </td>
      <td style="text-align:left">&#x53D6;&#x5F97;&#x6B64;element&#x5167;&#x6A19;&#x7C64;&#x540D;&#x7A31;&#x70BA;tagName&#x7684;
        <br
        />&#x6240;&#x6709;&#x5B50;&#x5143;&#x7D20;</td>
    </tr>
  </tbody>
</table>

## 🍵動態建立表格

{% tabs %}
{% tab title="DOM" %}
對應範例檔案07/30「getMore\_XML.html」「getMore\_XML.php」  
取得會員資料（僅字串相連）

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

