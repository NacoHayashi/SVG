# SVG Sharing


### SVG是什麼
可縮放向量圖形（Scalable Vector Graphics，縮寫：SVG）
SVG在2003年1月14日成為W3C的標準，並且是開放標準。
2011年發布了 SVG 1.1第2版

簡單來說是一種XML型態的向量圖，可以用於 Web 和其他環境。

``SVG 是活生生的物體，而點陣圖是物體的照片。``
--取自[設計師對 SVG 應該有的觀念](https://intersection.tw/%E8%A8%AD%E8%A8%88%E5%B8%AB%E5%B0%8D-svg-%E6%87%89%E8%A9%B2%E6%9C%89%E7%9A%84%E8%A7%80%E5%BF%B5-38ba64b48b32)


### 能支援的內容
- 基本向量:包括矩形(rect)、園(circle)、橢圓(ellipse)、多邊形(ploygon)、直線(line)、任意曲線(polyline)、路徑(path)等
- 嵌入式外部圖像，包括PNG、JPEG、SVG等 （但裡面塞像素圖其實沒啥意義)
- 文字對象

### 優缺點

#### 優點
 任意尺寸，不會破壞原本的圖的清晰度

||Png|SVG|
|--|--|--|
|32x32|<img src="./images/cat_32.png" alt="sample" />|<img src="./images/cat.svg" alt="sample" width="32px" height="32px"/>|
|100x100|<div><img src="./images/cat_32.png" alt="sample" width="100px" height="100px"/></div>|<img src="./images/cat.svg" alt="sample" width="100px" height="100px"/>|




- 檔案大小相較於其他圖片型態少很多 (因為決定一張影像（像是PNG或JPEG檔案大小的因素是解析度。3000x3000 的像素圖片一定比 300x300 的大)，而且細節越多(漸層、特效等等)也不太會增加太多檔案大小




#### 512 的png(59KB)
<img src="./images/cat_512.png" alt="sample" width="512px" height="512px"/>

#### 512 svg(25KB)
<img src="./images/cat.svg" alt="sample" width="512px" height="512px"/>



- 靈活性和多功能性高，可以做成動畫、跟CSS與JS搭配製作,還能直接使用在html上
- SVG圖形格式可以方便的建立文字索引， 能做內容的圖像搜尋
- 圖像文件可讀，易於修改和編輯
- 很多設計軟體可以直接輸出
- 基本使用在各瀏覽器都支援 (參考：https://caniuse.com/?search=Svg)

#### 缺點
- 部分操作在有些舊的瀏覽器可能不支援 
- 套件產出的svg不一定易讀易改
- 在電腦的資料夾下可能沒法縮圖預覽

### 網頁中的應用
- img 來源：可以在img Tag src 使用SVG （iframe, object, embed也能載用svg檔）
````
<img src='cat.svg' alt=''/>
````
- CSS 中使用：可以使用 background-image (如果没有固定尺寸， SVG會是元素高度與寬度100%) 
````
// Url 引入一個svg file
.svg-img {
    background-image: url('cat.svg');
}

// Url 使用data url把整個SVG檔案塞入 (注意後面要用編碼不然容易會造成瀏覽器判讀錯誤)
.svg-img-xml {
background-image: url(data:image/svg+xml,這邊放SVG的轉檔);
}
````
這位大大直接做好線上轉檔的小工具：[SVG在线压缩合并工具](https://www.zhangxinxu.com/sp/svgo/)
- 直接當HTML tag 使用
````
<svg width='100' heiight='100' xmlns='http://wwww.w3.org/2000/svg'>
  <title>Cat</title>
  <desc>Testt</desc>
  ...
</svg>    
````

### 基本結構
SVG的寬高決定它的大小(viewPort), viewBox ( min-x, min-y, width, height )
決定你看到的區域(有點像鏡頭你想要聚焦在哪個地方)
可以參考這篇解說[[技術分享] 理解 SVG 中的 Viewport 和 ViewBox－拖曳與縮放功能實做（上）](https://pjchender.blogspot.com/2017/03/svg-viewport-viewbox-zoomdrag.html)

ex :像是我想要只看貓頭我就把viewBox 調整成100 50 300 300

<svg width="90" height="90">       
     <image xlink:href="./images/cat_viewbox.svg" src="./images/cat_viewbox.svg" width="100" height="100"/>    
</svg>


#### SVG最基本的樣子是這樣的
````
<?xml version="1.0" encoding="UTF-8"?>
<svg width='100' heiight='100' xmlns='http://wwww.w3.org/2000/svg'>
  <title>Cat</title>
  <desc>Testt</desc>
  ...我這是內容物啊～
</svg>  

````
#### 常用控制顏色的參數
- fill: 填充顏色, 如果在Svg Tag 本身設置的fill 打
- stroke : 線的顏色

(如果是fll:currentColor 則會吃父層容器的顏色設定)

#### 基本內容元素
1. 圖形元素：``<rect>、<circle>、<ellipse>、<line>、<polyline>、<polygon>、 <path>``;
2. HTML元素：``<svg>, <embed>, <object>, <img> <iframe>``
3. 文字元素：``<text>``包住文字或是文字組, ``<tspan>``在``<text>``中控制單獨某文字,``<textpath>``在``<text>``中按照``<path>``的形狀排出文字





#### 組員們
1. ``<g>`` : 是一個群組概念，如果用過photoshop 之類的軟體，它就像一個圖層資料夾，裡面包著很多你畫出來的圖層(物件、路徑)，通常會設置一個專屬的id讓，每個組合還可以設置自己的``<title>``和``<desc>``供xml識別或是提供視障用戶的使用
  ````
  <?xml version="1.0" encoding="UTF-8"?>
  <svg width='100' heiight='100' xmlns='http://wwww.w3.org/2000/svg'>
    <title>Cat</title>
    <desc>Testt</desc>
    <g id='cat_head' style='fill:none; stroke:black'>
      <title>Cat head</title>
      <desc>貓的頭</desc>
      ...內容元素
    </g>

    <g id='cat_body' style='fill:none; stroke:black'>
    <title>Cat body</title>
      <desc>貓的身體</desc>
      ...內容元素
    </g>
  </svg>    
  ````
2. ``<use>``: 重複使用某個``<g>``的時候可以用use呼叫他出來，即使在不同的檔案都可以，只要在xlink:href屬性指定來源＋``<g>``的#id,就能使用,xy是控制位置要放哪
````
<svg xmlns='http://wwww.w3.org/2000/svg'>
  <use xlink:href='#cat_head' x='70' y='100'/>
</svg>
````
3.  ``<defs>``與``<symbol>``他們倆都比較像是模板，放在裡面的元素都會預設是看不到的，當你需要使用的時候在用``<use>``拿來用
````
  <?xml version="1.0" encoding="UTF-8"?>
  <svg width='100' heiight='100' xmlns='http://wwww.w3.org/2000/svg'>
    <title>Cat</title>
    <desc>Testt</desc>

    //這塊預設是看不到的
    <defs>
      <symbol id='cat_head' style='fill:none; stroke:black'>
        <title>Cat head</title>
        <desc>貓的頭</desc>
        ...內容元素
      </symbol>     
    </defs>

    //這塊預設是看得到的
     <g id='cat_body' style='fill:none; stroke:black'>
      <title>Cat body</title>
        <desc>貓的身體</desc>
        ...內容元素
      </g>

    //頭被我們呼喚出來了
     <use xlink:href='#cat_head'/>
  </svg> 
````
defs也可以是一個漸層的規則，可以在需要使用的圖形中使用
````
<?xml version="1.0" standalone="no"?>

<svg width="500" height="500" version="1.1"
xmlns="http://www.w3.org/2000/svg">

  //制定一個漸層範圍規則
  <defs>
      <linearGradient id="orange_red" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop offset="0%" style="stop-color:rgb(255,255,0);
      stop-opacity:1"/>
      <stop offset="100%" style="stop-color:rgb(255,0,0);
      stop-opacity:1"/>
      </linearGradient>
  </defs>

  // 這邊引用id #orange_red的規則去填色
  <ellipse cx="200" cy="190" rx="85" ry="55"
  style="fill:url(#orange_red)"/>
</svg>
````
範例參考：[记一次前端SVG实战知识分享会](https://segmentfault.com/a/1190000037490877)

### SVG 應用在 icon
目前有的方法有這幾種：
- Inline SVG : 直接將 SVG 放到畫面上。
  - 優點 ：保留最原始的設定，可以由CSS直接控制樣式，也不用request載入圖片。
  - 缺點： 可能會造成code雜亂，而且不是圖片檔沒有快取。 
- 設為CSS Background：設置一個class 在 background裡使用個別的SVG圖檔。來源可以是一個圖檔的url或是將SVG轉成 data url
  - 優點 ：
    - 畫面使用乾淨 (跟一般使用class一樣)
    - 可以被快取
    - data url 改顏色可以直接寫在url的svg裡面
  - 缺點： 
    - 圖檔需要request載入
    - 改顏色屬性需要到SVG檔案本身用ＣＳＳ改
    - 如果是data url 在hover的效果要再引入另一個data url
- `` <img> ``載入SVG來源：這是指使用 <img> 載入個別 SVG圖檔。如同上面所說的[網頁中的應用-img來源](#網頁中的應用)
  - 優點 ：
    - 畫面使用乾淨
    - 直接知道是個圖檔
    - 可以被快取
  - 缺點： 
    - 圖檔需要request載入。 
    - 沒法用css改樣式

- SVG Sprites：將多個SVG圖檔結合成一個SVG檔，使用時只要抓出想要的圖案就好，有以下兩種抓檔方式
  1. class backgroud position :這是指將 SVG Sprites 轉為 Data URI，再利用CSS背景定位顯示。如同上面所說的[網頁中的應用-css background data url 搭配css position](#網頁中的應用)
   - 優點 ：
      - 畫面使用乾淨
      - 減少HTTP Request
      - 檔案可經編碼後適度優化或縮小
      - 可以被快取
  - 缺點： 
    - position定位要另外紀錄且可能會錯誤
    - hover 樣式需要另外引入另一個data url 
    - 沒法用css改樣式
  2. SVG Symbols :並使用 SVG Symbols id來抓。如同上面所說的[SVG結構的範本組員-symbols 搭配use](#組員們)
  - 優點 ：
      - 畫面使用乾淨
      - 減少HTTP Request，多個icon只需要載入一個圖檔
      - 用use 指定圖檔id就可以抓出想要的icon
      - 可以用css改樣式, hover也不用重新載圖
      - 可以被快取
  - 缺點： 
    - 如果SVG Sprites 是外部檔案，可能需要解決快網域存取問題
  - 推薦快速製作SVG Sprites的套件 [svg-sprite-generate](https://github.com/frexy/svg-sprite-generator)

### 與Canvas 的比較
- Canvas 是用JS動態像素渲染，就像一個img畫布，裡面動自己的，比較適合動態渲染跟數據的繪製
- SVG 是用XML編寫，屬於HTML Dom的存在，比較適合靜態或圖像清晰度高要求的地方
詳細可以參考此篇[SVG 与 HTML5 的 canvas 各有什么优点，哪个更有前途？](https://www.zhihu.com/question/19690014)