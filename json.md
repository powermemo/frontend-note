---
description: 一種資料交換的格式
---

# JSON

## HTML的JSON

{% hint style="info" %}
兩種常見的方法

* `JSON.stringify(js物件) //物件轉字串`
* `JSON.parse(json字串)   //`
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
JSON.parse\(json字串\)

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
// 【result】obj.phone:03-4257387,03-168168,0933168168
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
 // 【result】obj.phone:[object Object]
 // 【result】obj.phone.H:03-168168
 // 【result】obj.phone.M:0933168168
```
{% endtab %}
{% endtabs %}

## PHP的JSON

{% hint style="info" %}
* `json_encode()`
* `json_decode()`
{% endhint %}

對應範例檔0804「json.php」

{% tabs %}
{% tab title="json\_encode" %}
json\_encode\(\)

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
json\_decode\(\)

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

