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

* 🔶CODEPEN\[連結\]



