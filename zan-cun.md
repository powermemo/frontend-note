# 暫存

## 拖曳圖片

![](.gitbook/assets/image%20%2841%29.png)

{% tabs %}
{% tab title="HTML" %}
```text
<div class="wrap">
  <div class="pics">
    <a href="https://google.com"><img src="https://picsum.photos/400/355/?random=9" alt=""></a>
    <a href="https://google.com"><img src="https://picsum.photos/400/355/?random=8" alt=""></a>
    <a href="https://google.com"><img src="https://picsum.photos/400/355/?random=7" alt=""></a>
    <a href="https://google.com"><img src="https://picsum.photos/400/355/?random=6" alt=""></a>
    <a href="https://google.com"><img src="https://picsum.photos/400/355/?random=5" alt=""></a>
    <a href="https://google.com"><img src="https://picsum.photos/400/355/?random=4" alt=""></a>
    <a href="https://google.com"><img src="https://picsum.photos/400/355/?random=86" alt=""></a>
    <a href="https://google.com"><img src="https://picsum.photos/400/355/?random=22" alt=""></a>
    <a href="https://google.com"><img src="https://picsum.photos/400/355/?random=567" alt=""></a>
    <a href="https://google.com"><img src="https://picsum.photos/400/355/?random=58" alt=""></a>
  </div>
  <button id="prev">＜</button>
  <button id="next">＞</button>
</div>
```
{% endtab %}

{% tab title="CSS" %}
```
*{
  margin: 0;
  padding: 0;
  font-size: 0;
/*   box-sizing:border-box; */
}
.wrap{
  position:relative;
/*   border: 5px solid ; */
  margin: auto;
  max-width: 450px;
}
.pics{
  display:flex;
  overflow-x: scroll;
}
.pics::-webkit-scrollbar{display:none;}
.pics img{
  max-width: 150px;
  cursor:-webkit-grab;
}
.wrap button{
  font-size: 20px;
  position:absolute;
  top:50%;
  height: 100%;
  padding: 5px;
  border: 0;
  background: rgba(0,0,0,0.5);
  color:white;
  font-weight: 900;
}
.wrap button:nth-child(2){
  left:0;
  transform:translate(-100%,-50%);
}
.wrap button:last-child{
  right:0;
  transform:translate(100%,-50%);
}
.active{
/*   transform:scale(1.1); */
  cursor:-webkit-grabbing;
}
```
{% endtab %}

{% tab title="JS" %}
```javascript
const pics = document.querySelector('.pics');
const prev = document.querySelector('#prev');
const next = document.querySelector('#next');
const img = document.querySelectorAll('.pics img');
let startX = 0;//起始位置
let startScroll = 0;//判斷捲動位置
// let startTime = 0;//滑動判斷
let moved = false;//防止圖片被拖曳

next.addEventListener('click',nextPageGo);
prev.addEventListener('click',prevPageGo);
pics.addEventListener('mousedown',startDrag);
pics.addEventListener('mousemove',draging);
pics.addEventListener('mouseup',stopDrag);
pics.addEventListener('mouseleave',stopDrag);
document.querySelectorAll('.pics a').forEach(dom=>{
  dom.addEventListener('click',function(e){if(moved){e.preventDefault();}})
})

function startDrag(e){
  moved = false;
  pics.classList.add('active')
  startX = e.pageX;
  startScroll = pics.scrollLeft;
  // startTime = new Date().getTime();
  img.forEach(i=>{
      i.style.cursor='-webkit-grabbing';
    })
}
function draging(e){
  e.preventDefault();
  if(pics.classList.contains('active')){
    moved = true;
    move = e.pageX - startX;
    pics.scrollLeft = startScroll - move*3;
    
  }
}
function stopDrag(e){
  pics.classList.remove('active');
  img.forEach(i=>{
    i.style.cursor='-webkit-grab';
  })
  //  if(new Date().getTime() - startTime <= 250){
  //   if(e.pageX > startX){
  //    console.log('swiper right');
  //   }else if(e.pageX < startX){
  //     console.log('swiper left');
  //   }
  // }
}
function nextPageGo(e){
  pics.scrollLeft += document.querySelector('img').width*2 ;
}
function prevPageGo(){
  pics.scrollLeft -= document.querySelector('img').width*2 ;
}

```
{% endtab %}
{% endtabs %}

## 假的購物車

![](.gitbook/assets/image%20%2842%29.png)

{% tabs %}
{% tab title="Plain Text" %}
```text
<button class="open">HA</button>
<div class="shoplist">
  <button class="close">X</button>
  <h2>購物清單</h2>
  <div class="wrap">
    <div class="item">
      <img src="https://picsum.photos/270/50" alt="">
      <div class="info">
        <h3>TITLE</h3>
        <p>$950</p>  
        <input type="number" min="1" value="1">
      </div>
      
      <button class="trash">垃圾</button>
    </div>
    <div class="item">
      <img src="https://picsum.photos/50/50" alt="">
      <div class="info">
        <h3>TITLE</h3>
        <p>$950</p>  
        <input type="number" min="1" value="1">
      </div>
      
      <button class="trash">垃圾</button>
    </div>
    <div class="item">
      <img src="https://picsum.photos/250/50" alt="">
      <div class="info">
        <h3>TITLE</h3>
        <p>$950</p>  
        <input type="number" min="1" value="1">
      </div>
      
      <button class="trash">垃圾</button>
    </div>
    <div class="item">
      <img src="https://picsum.photos/580/50" alt="">
      <div class="info">
        <h3>TITLE</h3>
        <p>$950</p>  
        <input type="number" min="1" value="1">
      </div>
      
      <button class="trash">垃圾</button>
    </div>
    <div class="item">
      <img src="https://picsum.photos/230/50" alt="">
      <div class="info">
        <h3>TITLE</h3>
        <p>$950</p>  
        <input type="number" min="0" value="1">
      </div>
      
      <button class="trash">垃圾</button>
    </div>
  </div>
  
</div>
<main>
  <div>1</div>
<div>2</div>
<div>3</div>
<div>4</div>
<div>5</div>
<div>6</div>
<div>7</div>
<div>8</div>
<div>9</div>
<div>10</div>
<div>11</div>
<div>12</div>
<div>13</div>
<div>14</div>
<div>15</div>
<div>16</div>
<div>17</div>
<div>18</div>
<div>19</div>
<div>20</div>
<div>21</div>
<div>22</div>
<div>23</div>
<div>24</div>
<div>25</div>
<div>26</div>
<div>27</div>
<div>28</div>
<div>29</div>
<div>30</div>
<div>31</div>
<div>32</div>
<div>33</div>
<div>34</div>
<div>35</div>
<div>36</div>
<div>37</div>
<div>38</div>
<div>39</div>
<div>40</div>
<div>41</div>
<div>42</div>
<div>43</div>
<div>44</div>
<div>45</div>
<div>46</div>
<div>47</div>
<div>48</div>
<div>49</div>
<div>50</div>
</main>

```
{% endtab %}

{% tab title="" %}
```
*{
  margin: 0;
  padding: 0;
}
button{
  border: 0  ;
  background: transparent;
}
button.open{
  position:fixed;
  display:block;
  bottom: 20px;
  right: 20px;
}
.shoplist{
  position:fixed;
  bottom: 30px;
  right: 30px;
  background: #520;
  height:450px;
  width:350px;
  border-radius: 5px;
  padding: 20px;
  padding-bottom: 50px;
  display:none;
}
button.close{
  position:absolute;
  right: 0;top: 0;
  font-size: 25px;
  font-weight: 700;
  line-height: 50px;
  width: 50px;
  border-radius: 0 5px 0 0 ;
  background: #cba;
}
.shoplist h2{
  text-align: center;
/*   border: 1px solid  ; */
  color: white;
  margin-bottom: 15px;
}
.shoplist .wrap{
  height: 85%;
  overflow-y:scroll;
}
.shoplist .wrap .item{
  display:flex;
  justify-content:space-between;
  margin-bottom: 15px;
}
.shoplist .wrap .item:nth-child(odd){
  background: #aaa;
}
.shoplist .wrap .item:nth-child(even){
  background: #ccc;
}
.shoplist .wrap .item img{
  height: 100px;
  width: 100px;
  object-fit:center;
}
.shoplist .wrap .item .info{
  flex-grow:1;
  padding-left: 15px;
  padding-top: 15px;
  display:flex;
  flex-direction:column;
}
.shoplist .wrap .item .info h3{
  overflow:hidden;
  display:inline-block;
}
.shoplist .wrap .item .info h3::-webkit-scrollbar {
  display: none ;
}
.shoplist .wrap .item .info input{
  max-width:50px;
  text-align:center;
}
.shoplist .wrap .item button{
  padding: 5px;
}
.shoplist .wrap .item button:hover{
  background: black;
  color: white;
}
.shownow{
  display:block;
}
```
{% endtab %}

{% tab title="" %}
```
$('button.open').click(function(){
  $('div.shoplist').addClass('shownow')
})
$('button.close').click(function(){
  $(this).parent().removeClass('shownow');
})
$('button.trash').click(function(){
  $(this).parent().css('display','none');
})
```
{% endtab %}
{% endtabs %}

## Alex頻道

* codepen\[[連結](https://codepen.io/achen224/pen/QBJNzq)\]
* 影片\[[連結](https://www.youtube.com/watch?v=XLegPUzpLrU)\]
* 
