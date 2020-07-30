# three js

學習手冊\(英文\)\[[連結](https://threejs.org/docs/)\]  
入門手冊\(中文\)\[[連結](https://read.douban.com/reader/ebook/7412854/)\]

* IT邦幫忙介紹\[[連結](https://ithelp.ithome.com.tw/articles/10199699)\] 
  * [官網範例](https://threejs.org/examples/)
  * [Learning Three.js](https://github.com/josdirksen/learning-threejs)
  * [Three.js 101 : Hello World! \(Part 1\)](https://medium.com/@necsoft/three-js-101-hello-world-part-1-443207b1ebe1)
  * [Three.js快速入門](https://www.itread01.com/articles/1476704140.html)

| \[3-[立方動畫](https://ithelp.ithome.com.tw/articles/10199702)\]\[[果](https://dezchuang.github.io/ironman-three.js/day03_helloThree/index.html)\] |  |  |  |  |  |  |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
|  |  |  |  |  |  |  |

## 簡介

![IT&#x90A6;&#x5E6B;&#x5FD9;&#xFF1A;&#x7528; Three.js &#x4F86;&#x7576;&#x500B;&#x5275;&#x4E16;&#x795E; \(01\)&#xFF1A;Three.js &#x7C21;&#x4ECB;](https://ithelp.ithome.com.tw/upload/images/20191129/20107572ZU8LbQsnv0.png)

* 場景（Scene）：例如`scene.add(...)`。
* 相機（Camera）：例如`switchCamera`。
* 物體（Objects）：例如`Points`、`Mesh`、`Geometry`、`Material`。
* 光源（Light）：不需要考慮光源即可被渲染在畫面上，例如 `MeshBasicMaterial` 、 `MeshNormalMaterial` ；能夠與光源互動的材質一般會用 `MeshLambertMaterial` 或 `MeshPhongMaterial` 。
* 渲染器（Renderer）：一般而言都是使用 `WebGLRenderer` 這個渲染器。



