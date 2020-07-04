---
description: 'https://javascript30.com/'
---

# Untitled

## 001 - Drum Kit鼓聲

![](https://res.cloudinary.com/wesbos/image/fetch/q_auto,f_auto/https://s3.amazonaws.com/js30-cdn/small0.jpg)

* 原始碼\[[連結](https://github.com/wesbos/JavaScript30/tree/master/01%20-%20JavaScript%20Drum%20Kit)\] 原教學影片\[[連結](https://courses.wesbos.com/account/access/5ef942df055a68151fb7da3b/view/194130650)\] Alex影片教學\[[連結](https://youtu.be/f2ttaeDHzwE?t=1080)\] 
* 查詢keycode\[[連結](https://keycode.info/)\]
* getElement\(s\)與querySelector的不同\[[連結](https://www.itread01.com/content/1558613044.html)\] 、 基礎認識querySelector\[[連結](https://ithelp.ithome.com.tw/articles/10211605)\]
* 🔶CODEPEN\[[連結](https://codepen.io/ch-zhuchu/pen/XWXzZOY)\]

{% tabs %}
{% tab title="JS" %}
```javascript
// ALEX版本
/*兩個function、兩個addEventListenter*/
function playHandler(e){
 //play music
 const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`)
 if(!audio) return;
 audio.currentTime = 0;
 audio.play()
 // style
 const key = document.querySelector(`div[data-key="${e.keyCode}"]`)
 key.classList.add('playing')
 console.log(audio,key)
}
  
function transitionendHandler(e){
  if(e.propertyName === 'transform'){
    e.currentTarget.classList.remove('playing')
  }
}

window.addEventListener('keydown',playHandler)
document.querySelectorAll('.key').forEach(function(e){
  e.addEventListener('transitionend',transitionendHandler)
})
```
{% endtab %}
{% endtabs %}

## 002 - JS + CSS Clock時鐘

![](https://res.cloudinary.com/wesbos/image/fetch/q_auto,f_auto/https://s3.amazonaws.com/js30-cdn/small1.jpg)

* 🔶CODEPEN\[[連結](https://codepen.io/ch-zhuchu/pen/bGEYLyB)\]

{% tabs %}
{% tab title="CSS" %}
```css
html {
  background: #018DED url(https://unsplash.it/1500/1000?image=881&blur=5);
  background-size: cover;
  font-family: 'helvetica neue';
  text-align: center;
  font-size: 10px;
}

body {
  margin: 0;
  font-size: 2rem;
  display: flex;
  flex: 1;
  min-height: 100vh;
  align-items: center;
}

.clock {
  width: 30rem;
  height: 30rem;
  border: 20px solid white;
  border-radius: 50%;
  margin: 50px auto;
  position: relative;
  padding: 2rem;
  box-shadow:
    0 0 0 4px rgba(0,0,0,0.1),
    inset 0 0 0 3px #EFEFEF,
    inset 0 0 10px black,
    0 0 10px rgba(0,0,0,0.2);
}

.clock-face {
  position: relative;
  width: 100%;
  height: 100%;
  transform: translateY(-3px); /* account for the height of the clock hands */
}
.clock-face::after {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
  width: 30px;
  height: 30px;
  background: white;
  border-radius: 50%;
}
.hand {
  position: absolute;
  width: 100%;
  height: 100%;
}
/*秒針樣式*/
.second-hand::after{
  content: '';
  display: block;
  position: absolute;
  bottom: 50%;
  left: 50%;
  transform: translate(-50%,-0%);
  background: lightblue;
  width: 5px;
  height: 50%;
}
/*分針樣式*/
.min-hand::after{
  content: '';
  display: block;
  position: absolute;
  bottom: 50%;
  left: 50%;
  transform: translate(-50%,-0%);
  background: brown;
  width: 10px;
  height: 40%;
}
/*時針樣式*/
.hour-hand::after{
  content: '';
  display: block;
  position: absolute;
  bottom: 50%;
  left: 50%;
  transform: translate(-50%,-0%);
  background: salmon;
  width: 15px;
  height: 30%;
}
```
{% endtab %}

{% tab title="JS" %}
```javascript
//ALEX版本
const sec = document.querySelector('.second-hand');
const min = document.querySelector('.min-hand');
const hur = document.querySelector('.hour-hand');
function setClock(){
  let data = new Date();
  let secDeg = data.getSeconds() * 6;//360deg÷60=6deg
  let minDeg = data.getMinutes() * 6 + data.getSeconds() * 6 / 60;
  //👆360deg÷60格=6deg。每兩格(分鐘)之間6度，這6度分配給60秒（每跑1秒轉動的度數）
  let hurDeg = data.getHours() * 30 + data.getMinutes() * 30 / 60;
  //👆360deg÷12格=30deg。每兩格(小時)之間30度，這30度分配給60分鐘（每跑1分鐘轉動的度數）
  sec.style.transform = `rotate(${secDeg}deg)`;
  min.style.transform = `rotate(${minDeg}deg)`;
  hur.style.transform = `rotate(${hurDeg}deg)`;
}
setClock();//初始化畫面
/*計時器 setInterval、setTimeout、requestAnimationFrame*/
// setInterval(setClock,1000);//👈【1】每1000毫秒執行一次(設定間隔，持續執行)

/* setTimeout(timeoutHandler,1000);//👈【2】設定延遲，執行一次
function timeoutHandler(){
  setClock()
  setTimeout(timeoutHandler,1000);
}*/
window.requestAnimationFrame(animationHandler);//👈【3】處理畫面更新的setTimeout
function animationHandler(){
  setClock();
  window.requestAnimationFrame(animationHandler);
}
//canvas動畫，強烈建議使用「requestAnimationFrame」


//IIFE有興趣可以查一下XD
```
{% endtab %}
{% endtabs %}

## 003 - CSS Variables 畫盤

![](https://res.cloudinary.com/wesbos/image/fetch/q_auto,f_auto/https://s3.amazonaws.com/js30-cdn/small2.jpg)

* 🔶CODEPEN\[[連結](https://codepen.io/ch-zhuchu/pen/abdVGNd)\]

{% tabs %}
{% tab title="JS" %}
```javascript
/*ALEX版本
 *定義
 *函數
 *forEach事件聆聽功能*/
 ;(function(){//IIFC
  const inputs = document.querySelectorAll('.controls input');
  inputs.forEach(function(t){
    t.addEventListener('change',styleHandler)
    t.addEventListener('mousemove',styleHandler)
  })
  function styleHandler(){
    //👇方法【1】
    //   switch(this.name){
    //     case 'spacing':
    //       document.querySelector('img').style.padding = this.value + 'px'
    //       break
    //     case 'blur':
    //       document.querySelector('img').style.filter = `blur(${this.value}px)`
    //       break
    //     case 'base'://color
    //       document.querySelector('img').style.background = this.value
    //       document.querySelector('.hl').style.color = this.value
    //       break
    //   };

    //👇方法【2】
    //變數「unit」解釋：如果dataset有值就用dataset的值，如果dataset沒有值就不要給
    const unit = this.dataset.sizing || ''
    document.documentElement.style.setProperty(`--${this.name}`,this.value + unit) 
  }

  /*對應到HTML的三種寫法
       * 1.document.querySelector('html')
       * 2.document.querySelector(':root')
       * 3.document.documentElement*/


})()

```
{% endtab %}
{% endtabs %}

## 004 - console練習

![](https://res.cloudinary.com/wesbos/image/fetch/q_auto,f_auto/https://s3.amazonaws.com/js30-cdn/small3.jpg)

* 🔶CODEPEN\[[連結](https://codepen.io/ch-zhuchu/pen/oNbodzZ)\]

## 005 - Image Gallery圖片牆

![](https://res.cloudinary.com/wesbos/image/fetch/q_auto,f_auto/https://s3.amazonaws.com/js30-cdn/small4.jpg)

* 🔶CODEPEN\[[連結](https://codepen.io/ch-zhuchu/pen/wvMpwaL)\]

{% tabs %}
{% tab title="css" %}
```text
html {
  box-sizing: border-box;
  background: #ffc600;
  font-family: 'helvetica neue';
  font-size: 20px;
  font-weight: 200;
}

body {
  margin: 0;
}

*, *:before, *:after {
  box-sizing: inherit;
}

.panels {
  min-height: 100vh;
  overflow: hidden;
  display: flex;
}

.panel {
  flex: 1;/*每塊區域占一等份*/
  display:flex;/*讓內文可以製中*/
  flex-direction:column;
  justify-content:center;
  background: #6B0F9C;
  box-shadow: inset 0 0 0 5px rgba(255,255,255,0.1);
  color: white;
  text-align: center;
  align-items: center;
  /* Safari transitionend event.propertyName === flex */
  /* Chrome + FF transitionend event.propertyName === flex-grow */
  transition:
    font-size 0.7s cubic-bezier(0.61,-0.19, 0.7,-0.11),
    flex 0.7s cubic-bezier(0.61,-0.19, 0.7,-0.11),
    background 0.2s;
  font-size: 20px;
  background-size: cover;
  background-position: center;
}

.panel1 { background-image:url(https://source.unsplash.com/gYl-UtwNg_I/1500x1500); }
.panel2 { background-image:url(https://source.unsplash.com/rFKUFzjPYiQ/1500x1500); }
.panel3 { background-image:url(https://images.unsplash.com/photo-1465188162913-8fb5709d6d57?ixlib=rb-0.3.5&q=80&fm=jpg&crop=faces&cs=tinysrgb&w=1500&h=1500&fit=crop&s=967e8a713a4e395260793fc8c802901d); }
.panel4 { background-image:url(https://source.unsplash.com/ITjiVXcwVng/1500x1500); }
.panel5 { background-image:url(https://source.unsplash.com/3MNzGlQM7qs/1500x1500); }

/* Flex Children */
.panel > * {
  flex:1;/*每個物件占一等份*/
  margin: 0;
  width: 100%;
  transition: transform 0.5s;
}

.panel p {
  text-transform: uppercase;
  font-family: 'Amatic SC', cursive;
  text-shadow: 0 0 4px rgba(0, 0, 0, 0.72), 0 0 14px rgba(0, 0, 0, 0.45);
  font-size: 2em;
  display:flex;
  justify-content:center;
  align-items:center;
}

.panel > *:first-child{
  transform:translateY(-100%);
}
.panel > *:last-child{
  transform:translateY(100%);
}

.panel.open-active > *:first-child{
  transform:translateY(0%);
}
.panel.open-active > *:last-child{
  transform:translateY(0%);
}




.panel p:nth-child(2) {
  font-size: 4em;
}

.panel.open {
  font-size: 40px;
  flex:3;
}
```
{% endtab %}

{% tab title="html" %}
```
<div class="panels">
  <div class="panel panel1">
    <p>Hey</p>
    <p>Let's</p>
    <p>Dance</p>
  </div>
  <div class="panel panel2">
    <p>Give</p>
    <p>Take</p>
    <p>Receive</p>
  </div>
  <div class="panel panel3">
    <p>Experience</p>
    <p>It</p>
    <p>Today</p>
  </div>
  <div class="panel panel4">
    <p>Give</p>
    <p>All</p>
    <p>You can</p>
  </div>
  <div class="panel panel5">
    <p>Life</p>
    <p>In</p>
    <p>Motion</p>
  </div>
</div>
```
{% endtab %}

{% tab title="JS" %}
```javascript
;(function(){
  const panels = document.querySelectorAll('.panel');/*這不是陣列！*/
  panels.forEach(pl =>{
    pl.addEventListener('click',openHandeler);  
    pl.addEventListener('transitionend',transitionendHandeler); /*transitionend過場結束之後*/
  })
  function openHandeler(){
    this.classList.toggle('open');
  }
  function transitionendHandeler(e){
    console.log(e);
    /*如果找到flex的話*/
    if(e.propertyName.indexOf('flex') !== -1){/*會依照屬性的數量觸發*/
      /*就是說..沒有if找，當「open-active」CSS屬性為雙數時「toggle」就會被抵銷...*/
      this.classList.toggle('open-active');
    }
  }
  
})()
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
JS：`classList.add()、classList.remove()`、`classList.toggle()`  
JQ：`addClass()`、`removeClass()`、`toggleClass()`
{% endhint %}

## 006 - Ajax Type Ahead

![](https://res.cloudinary.com/wesbos/image/fetch/q_auto,f_auto/https://s3.amazonaws.com/js30-cdn/small5.jpg)

{% tabs %}
{% tab title="HTML" %}
```text
<form class="search-form">
    <input type="text" class="search" placeholder="City or State">
    <ul class="suggestions">
      <li>Filter for a city</li>
      <li>or a state</li>
    </ul>
  </form>
```
{% endtab %}

{% tab title="CSS" %}
```
html {
  box-sizing: border-box;
  background: #ffc600;
  font-family: 'helvetica neue';
  font-size: 20px;
  font-weight: 200;
}

*, *:before, *:after {
  box-sizing: inherit;
}

input {
  width: 100%;
  padding: 20px;
}

.search-form {
  max-width: 400px;
  margin: 50px auto;
}

input.search {
  margin: 0;
  text-align: center;
  outline: 0;
  border: 10px solid #F7F7F7;
  width: 120%;
  left: -10%;
  position: relative;
  top: 10px;
  z-index: 2;
  border-radius: 5px;
  font-size: 40px;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.12), inset 0 0 2px rgba(0, 0, 0, 0.19);
}

.suggestions {
  margin: 0;
  padding: 0;
  position: relative;
  /*perspective: 20px;*/
}

.suggestions li {
  background: white;
  list-style: none;
  border-bottom: 1px solid #D8D8D8;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.14);
  margin: 0;
  padding: 20px;
  transition: background 0.2s;
  display: flex;
  justify-content: space-between;
  text-transform: capitalize;
}

.suggestions li:nth-child(even) {
  transform: perspective(100px) rotateX(3deg) translateY(2px) scale(1.001);
  background: linear-gradient(to bottom,  #ffffff 0%,#EFEFEF 100%);
}

.suggestions li:nth-child(odd) {
  transform: perspective(100px) rotateX(-3deg) translateY(3px);
  background: linear-gradient(to top,  #ffffff 0%,#EFEFEF 100%);
}

span.population {
  font-size: 15px;
}

.hl {
  background: #ffc600;
}
```
{% endtab %}

{% tab title="JS" %}
```
const endpoint = 'https://gist.githubusercontent.com/Miserlou/c5cd8364bf9b2420bb29/raw/2bf258763cdddd704f8ffd3ea9a3e81d25e2c6f6/cities.json';
//↓Alex的方式
// let req = new XMLHttpRequest();
// req.addEventListener('load',requestHandler);
// req.open('get',endpoint);
// req.send();
// function requestHandler(){
//   console.log(JSON.parse(this.reponse));
// }

//↓原作者的方式
const cities =[];
fetch(endpoint)
  .then(blob => blob.json())
  .then(data => cities.push(...data));

let cities2 = null'
fetch(endpoing)
  .then(blob => blob.json())
  .then(data => (cities2 = data));
```
{% endtab %}
{% endtabs %}

\(還沒寫完....\)

## 008 - Fun with HTML5 Canvas小畫家

![](https://res.cloudinary.com/wesbos/image/fetch/q_auto,f_auto/https://s3.amazonaws.com/js30-cdn/small7.jpg)

{% tabs %}
{% tab title="HTML" %}
```text
<canvas id="draw" width="800" height="800"></canvas>
```
{% endtab %}

{% tab title="CSS" %}
```
html, body {
 margin: 0;
}
```
{% endtab %}

{% tab title="JS" %}
```javascript
;(function(){
  let canvas = document.querySelector('#draw');
  let ctx = canvas.getContext('2d');
  let colorDeg = 0
  let lineWidth = 25
  let direction = 1
  ctx.strokeStyle = `hsl(${colorDeg},100%,50%)`;/*線條顏色*/
  ctx.lineWidth = lineWidth;/*線條寬度*/
  ctx.lineCap = 'round';/*線條邊邊*/
  ctx.lineJoin = 'round';/*線條轉角*/
  
  let drawing = false;/*繪圖狀態*/
  let x=0,y=0;/*xy軸起始值*/
  canvas.addEventListener('mousedown',(e)=>{
    drawing = true;
    //當滑鼠按下，紀錄xy軸
    [x,y] = [e.offsetX,e.offsetY];
    ctx.beginPath();
    ctx.moveTo(x,y);
    ctx.lineTo(x,y);
    ctx.stroke();
  })
  canvas.addEventListener('mousemove',(e)=>{
    //當游標動，會一直抓位置，所以...
    if(!drawing) return;
    console.log(drawing); 
    
    ctx.beginPath();//設定起始繪圖
    colorDeg = colorDeg<360? colorDeg+.5:0;
    ctx.strokeStyle = `hsl(${colorDeg},100%,50%)`;
    if(lineWidth<1 || lineWidth>50){direction*=-1;}
    lineWidth += direction;
    ctx.lineWidth = lineWidth;
    ctx.moveTo(x,y);//將起始點設定為滑鼠按下的位置
    ctx.lineTo(e.offsetX,e.offsetY);
      [x,y] = [e.offsetX,e.offsetY];
    ctx.stroke();//開始繪圖
  })
  document.addEventListener('mouseup',()=>{
    drawing = false;
  })
  //當滑鼠離開畫布範圍 
  canvas.addEventListener('mouseleave',()=>{
    drawing = false;
  })
})()
```
{% endtab %}
{% endtabs %}

## 010 - Hold Shift to Check Multiple Checkboxes按住shift選取區間

![](https://res.cloudinary.com/wesbos/image/fetch/q_auto,f_auto/https://s3.amazonaws.com/js30-cdn/small9.jpg)

{% tabs %}
{% tab title="HTML" %}
```text
<div class="inbox">
  <div class="item">
    <input type="checkbox">
    <p>This is an inbox layout.</p>
  </div>
  <div class="item">
    <input type="checkbox">
    <p>Check one item</p>
  </div>
  <div class="item">
    <input type="checkbox">
    <p>Hold down your Shift key</p>
  </div>
  <div class="item">
    <input type="checkbox">
    <p>Check a lower item</p>
  </div>
  <div class="item">
    <input type="checkbox">
    <p>Everything in between should also be set to checked</p>
  </div>
  <div class="item">
    <input type="checkbox">
    <p>Try to do it without any libraries</p>
  </div>
  <div class="item">
    <input type="checkbox">
    <p>Just regular JavaScript</p>
  </div>
  <div class="item">
    <input type="checkbox">
    <p>Good Luck!</p>
  </div>
  <div class="item">
    <input type="checkbox">
    <p>Don't forget to tweet your result!</p>
  </div>
</div>
```
{% endtab %}

{% tab title="CSS" %}
```
html {
  font-family: sans-serif;
  background: #ffc600;
}

.inbox {
  max-width: 400px;
  margin: 50px auto;
  background: white;
  border-radius: 5px;
  box-shadow: 10px 10px 0 rgba(0,0,0,0.1);
}

.item {
  display: flex;
  align-items: center;
  border-bottom: 1px solid #F1F1F1;
}

.item:last-child {
  border-bottom: 0;
}

input:checked + p {
  background: #F9F9F9;
  text-decoration: line-through;
}

input[type="checkbox"] {
  margin: 20px;
}

p {
  margin: 0;
  padding: 20px;
  transition: background 0.2s;
  flex: 1;
  font-family:'helvetica neue';
  font-size: 20px;
  font-weight: 200;
  border-left: 1px solid #D1E2FF;
}
```
{% endtab %}

{% tab title="JS" %}
```

```
{% endtab %}
{% endtabs %}

## 011 - Custom HTML5 Video Player

![](https://res.cloudinary.com/wesbos/image/fetch/q_auto,f_auto/https://s3.amazonaws.com/js30-cdn/small10.jpg)



## 013 - Slide In on Scroll

![](https://res.cloudinary.com/wesbos/image/fetch/q_auto,f_auto/https://s3.amazonaws.com/js30-cdn/small12.jpg)

## 015 - LocalStorage and Event Delegation

![](https://res.cloudinary.com/wesbos/image/fetch/q_auto,f_auto/https://s3.amazonaws.com/js30-cdn/small14.jpg)

## 016 - CSS Text Shadow Mouse Move Effect

![](https://res.cloudinary.com/wesbos/image/fetch/q_auto,f_auto/https://s3.amazonaws.com/js30-cdn/small15.jpg)

## 017 - Sorting Band Names without articles

![](https://res.cloudinary.com/wesbos/image/fetch/q_auto,f_auto/https://s3.amazonaws.com/js30-cdn/small16.jpg)

## 019 - Unreal Webcam Fun

![](https://res.cloudinary.com/wesbos/image/fetch/q_auto,f_auto/https://s3.amazonaws.com/js30-cdn/small18.jpg)



## 020 - Native Speech Recognition

![](https://res.cloudinary.com/wesbos/image/fetch/q_auto,f_auto/https://s3.amazonaws.com/js30-cdn/small19.jpg)

## 021 - Geolocation based Speedometer and Compass

![](https://res.cloudinary.com/wesbos/image/fetch/q_auto,f_auto/https://s3.amazonaws.com/js30-cdn/small20.jpg)

## 022 - Follow Along Links

![](https://res.cloudinary.com/wesbos/image/fetch/q_auto,f_auto/https://s3.amazonaws.com/js30-cdn/small21.jpg)

## 023 - Speech Synthesis

![](https://res.cloudinary.com/wesbos/image/fetch/q_auto,f_auto/https://s3.amazonaws.com/js30-cdn/small22.jpg)

## 024 - Sticky Nav

![](https://res.cloudinary.com/wesbos/image/fetch/q_auto,f_auto/https://s3.amazonaws.com/js30-cdn/small23.jpg)

## 026 - Stripe Follow Along Dropdown

![](https://res.cloudinary.com/wesbos/image/fetch/q_auto,f_auto/https://s3.amazonaws.com/js30-cdn/small25.jpg)

## 027 - Click and Drag to Scroll

![](https://res.cloudinary.com/wesbos/image/fetch/q_auto,f_auto/https://s3.amazonaws.com/js30-cdn/small26.jpg)

## 028 - Video Speed Controller UI

![](https://res.cloudinary.com/wesbos/image/fetch/q_auto,f_auto/https://s3.amazonaws.com/js30-cdn/small27.jpg)

## 029 - Countdown Clock

![](https://res.cloudinary.com/wesbos/image/fetch/q_auto,f_auto/https://s3.amazonaws.com/js30-cdn/small28.jpg)

## 030 - Whack A Mole Game

![](https://res.cloudinary.com/wesbos/image/fetch/q_auto,f_auto/https://s3.amazonaws.com/js30-cdn/small29.jpg)



