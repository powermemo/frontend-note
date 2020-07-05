# 暫存

## 拖曳圖片

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



