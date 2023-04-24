---
title: CSS 基础知识
---

## 标签样式

::: tip 参考资料

- [W3school-CSS](https://www.w3school.com.cn/css/index.asp)
- [菜鸟教程-CSS](https://www.runoob.com/css/css-tutorial.html)
- [绿叶学习网-CSS](http://www.lvyestudy.com/les_cj/css_list.aspx)

以后可以记录一些常用的
:::

## CSS 选择器

- 基础选择器
- 伪类选择器

<img :src="$withBase('/frontend/css/CSS基础选择器-1.jpg')" alt="基础选择器">

<img :src="$withBase('/frontend/css/CSS伪类选择器-2.jpg')" alt="伪类选择器">

## CSS 哪些属性可以继承？

css 继承特性主要是指文本方面的继承，盒模型相关的属性基本没有继承特性。

不可继承的：
`display、margin、border、padding、background、height、min-height、max-height、width、min-width、max-width、overflow、position、top、bottom、left、right、z-index、float、clear、 table-layout、vertical-align、page-break-after、page-bread-before和unicode-bidi。`

所有元素可继承的：
`visibility 和 cursor`

终极块级元素可继承的：
`text-indent 和 text-align`

内联元素可继承的：
`letter-spacing、word-spacing、white-space、line-height、color、font、font-family、font-size、font-style、font-variant、font-weight、text-decoration、text-transform、direction`

列表元素可继承的：
`list-style、list-style-type、list-style-position、list-style-image`

## 盒模型

### 基本概念

所有 HTML 元素可以看作盒子，在 CSS 中，"box model"这一术语是用来设计和布局时使用。

CSS 盒模型本质上是一个盒子，封装周围的 HTML 元素，它包括：边距，边框，填充，和实际内容。

盒模型允许我们在其它元素和周围元素边框之间的空间放置元素。

下面的图片说明了盒子模型(Box Model)：

<img :src="$withBase('/frontend/css/imgs/box-model.gif')" alt="box-model.gif">

不同部分的说明：

- margin(外边距) - 清除边框外的区域，外边距是透明的。
- border(边框) - 围绕在内边距和内容外的边框。
- padding(内边距) - 清除内容周围的区域，内边距是透明的。
- content(内容) - 盒子的内容，显示文本和图像。

**盒子在标准流中的定位原则：**

margin 控制的是盒子与盒子之间的距离，padding 存在于盒子的内部它不涉及与其他盒子之间的关系和相互影响问题，因此要精确控制盒子的位置，就必须对 margin 有更深入的了解。

**（1）行内元素之间的水平 margin**

当两个行内元素紧邻时，它们之间的距离为第一个元素的右 margin 加上第二元素的左 margin。

**（2）块级元素之间的竖直 margin**

两个竖直排列的块级元素，它们之间的垂直距离不是上边的第一个元素的下 margin 和第二个元素的上 margin 的总和，**而是两者中的较大者**。这在实际制作网页的时候要特别注意。

**（3）嵌套盒子之间的 margin**

这时子块的 margin 以父块的 content 为参考进行排列。

**（4）margin 设为负值**

会使设为负数的块向相反的方向移动，甚至会覆盖在另外的块上。

### 标准盒模型和 IE 盒模型的区别

#### 标准盒模型

<img :src="$withBase('/frontend/css/imgs/标准盒模型.png')" alt="标准盒模型.png">

标准盒模型（内容盒子）：宽高都指 content，不包括 padding 和 border；

它所说的 width 一般只包含内容,并且盒子的大小会以内容优先，自动扩展，子元素可以撑开父元素.

- 设置标准盒模型：`box-sizing:content-box;`

一般在现代浏览器中使用的都是 标准盒模型 content-box。

#### IE 盒模型

<img :src="$withBase('/frontend/css/imgs/IE盒模型.png')" alt="IE盒模型.png">

IE 盒模型又称怪异盒模型（边框盒子）：宽高是指 content+padding+border 的总的宽高；

- 设置 IE 盒模型：`box-sizing:border-box;`

一般在 IE 浏览器中默认为这种怪异盒模型，但是由于其自身的特殊性，手机页面中也有使用怪异盒模型。怪异盒模型中，父元素的盒模型确定，子元素无法撑开父元素的盒模型。

### 获取盒模型的宽高

以下 dom 是指通过 JS 获取到的，比如`getElementById`

`dom.style.width/height`

- 只能取内联样式中的的宽和高

`dom.currentStyle.width/height`

- 三种设置方式设置的宽高都可以取到，但是只支持 IE 浏览器

`window.getComputedStyle(dom).width/height`

- 三种设置方式设置的宽高都可以取到，兼容 firefox 和 chrome,相比上一种通用性更好一些

`dom.getBoundingClientRect().width/height`

- 适用场所：计算一个元素的绝对位置，相对于视窗 viewport 的左顶点的绝对位置，dom.getBoundingClientRect()方法可以拿到 left, top, right, bottom, x, y, width, and height

[MDN-getBoundingClientRect()](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/getBoundingClientRect)

### 实例题（根据盒模型解释边距重叠）

#### 父子元素：子元素的 height=100px；marign-top=10px；请问父元素的高度是？

下面的代码片段显示子元素和父元素的高度都是 100px；

若给父元素加上 overflow:hidden;（BFC），则子元素的高度为 100 不变，父元素的高度为 110px;

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title></title>
  </head>
  <body>
    <section id="sec">
      <style>
        * {
          margin: 0;
          padding: 0;
        }

        #sec {
          background: #f00;
        }

        .child {
          height: 100px;
          margin-top: 10px;
          background: yellow;
        }
      </style>
      <article class="child"></article>
    </section>
  </body>
</html>
```

#### 兄弟元素：若为上下分布，则大的 margin 兼容小的 margin；若为左右分布，则相加；

**上下分布: 以下代码片段中，elderBrother 和 youngerBrother 之间的上下间距是 30px；**

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title></title>
  </head>
  <body>
    <section id="sect">
      <style>
        * {
          margin: 0;
          padding: 0;
        }

        #sect article {
          height: 200px;
        }

        .elderBrother {
          margin-bottom: 30px;
          background: #f00;
        }

        .youngerBrother {
          margin-top: 10px;
          background: yellow;
        }
      </style>
      <article class="elderBrother"></article>
      <article class="youngerBrother"></article>
    </section>
  </body>
</html>
```

**左右分布：以下代码片段中，elderBrother 和 youngerBrother 之间的左右间距是 40px；**

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title></title>
  </head>
  <body>
    <section id="sect">
      <style>
        * {
          margin: 0;
          padding: 0;
        }

        #sect article {
          height: 100px;
          width: 300px;
          display: inline-block;
        }

        .elderBrother {
          margin-bottom: 30px;
          background: #f00;
        }

        .youngerBrother {
          margin-top: 10px;
          background: yellow;
        }
      </style>
      <article class="elderBrother"></article>
      <article class="youngerBrother"></article>
    </section>
  </body>
</html>
```

## BFC(边距重叠解决方案)

- BFC 的基本概念
- BFC 的布局规则
- 如何创建 BFC
- BFC 使用场景

### BFC 的基本概念

Block Formatting Context, 块级格式化上下文，一个独立的块级渲染区域，该区域拥有一套渲染规格来约束块级盒子的布局.
简单来说就是一个独立的盒子，并且这个盒子里的布局不受外部影响，也不会影响到外部元素。

### BFC 的布局规则

1. 内部的 Box 会在垂直方向，一个接一个地放置。
2. Box 垂直方向的距离由 margin 决定。属于同一个 BFC 的两个相邻 Box 的 margin 会发生重叠
3. 每个元素的 margin box 的左边， 与包含块 border box 的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。
4. BFC 的区域不会与 float box 重叠。
5. BFC 就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
6. 计算 BFC 的高度时，浮动元素也参与计算

[MDN-块格式化上下文](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)

- 块格式化上下文对浮动定位（参见  float）与清除浮动（参见  clear）都很重要。
- 浮动定位和清除浮动时只会应用于同一个 BFC 内的元素。
- 浮动不会影响其它 BFC 中元素的布局，而清除浮动只能清除同一 BFC 中在它前面的元素的浮动。
- 外边距折叠（Margin collapsing）也只会发生在属于同一 BFC 的块级元素之间。

#### 补充：包含块

[MDN-布局和包含块](https://developer.mozilla.org/zh-CN/docs/Web/CSS/All_About_The_Containing_Block)

[包含块](https://blog.csdn.net/u013217071/article/details/60132286)

**确定包含块**

---确定一个元素的包含块的过程完全依赖于这个元素的 position 属性：

1. 如果 position 属性为 static 或 relative ，包含块就是由它的最近的祖先块元素（比如说 inline-block, block 或 list-item 元素）或格式化上下文(比如说 a table container, flex container, grid container, or the block container itself)的内容区的边缘组成的。

2. 如果 position 属性为 absolute ，包含块就是由它的最近的 position 的值不是 static （也就是值为 fixed, absolute, relative 或 sticky）的祖先元素的内边距区的边缘组成。

3. 如果 position 属性是 fixed，在连续媒体的情况下(continuous media)包含块是 viewport ,在分页媒体(paged media)下的情况下包含块是分页区域(page area)。

4. 如果 position 属性是 absolute 或 fixed，包含块也可能是由满足以下条件的最近父级元素的内边距区的边缘组成的：

- A transform or perspective value other than none
- A will-change value of transform or perspective
- A filter value other than none or a will-change value of filter(only works on Firefox).
- A contain value of paint (例如: contain: paint;)

### 如何创建 BFC

[MDN-块格式化上下文](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)

1. **根元素 html**
2. **浮动元素（元素的  float  不是  none）**
3. **绝对定位元素（元素的  position  为  absolute  或  fixed）**
4. **行内块元素（元素的  display  为  inline-block）**
5. **表格单元格（元素的  display 为  table-cell，HTML 表格单元格默认为该值）**
6. **表格标题（元素的  display  为  table-caption，HTML 表格标题默认为该值）**
7. 匿名表格单元格元素（元素的  display 为  table、table-row、 table-row-group、table-header-group、table-footer-group（分别是 HTML table、row、tbody、thead、tfoot 的默认属性）或  inline-table）
8. **overflow  值不为  visible  的块元素**
9. display  值为  flow-root  的元素
10. contain  值为  layout、content 或  paint  的元素
11. **弹性元素（display 为  flex  或  inline-flex 元素的直接子元素）**
12. **网格元素（display 为  grid  或  inline-grid  元素的直接子元素）**
13. 多列容器（元素的  column-count  或  column-width  不为  auto，包括  column-count  为  1）
14. column-span  为  all  的元素始终会创建一个新的 BFC，即使该元素没有包裹在一个多列容器中（标准变更，Chrome bug）。

### BFC 常见作用

#### 解决浮动导致父元素高度塌陷问题

在通常情况下父元素的高度会被子元素撑开，而在这里因为其子元素为浮动元素所以父元素发生了高度坍塌，上下边界重合。这时就可以用 BFC 来清除浮动了。

<img :src="$withBase('/frontend/css/imgs/BFC-2-0.png')" alt="BFC-2-0.png">

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title></title>
  </head>
  <body>
    <section>
      <style>
        .par {
          border: 5px solid red;
          width: 1000px;
          /* 生成BFC，把浮动元素的高度计算在内，变相地清除了内部浮动 */
          overflow: hidden;
        }
        .child {
          border: 5px solid blue;
          float: left;
          height: 100px;
          width: 100px;
        }
      </style>
      <div class="par">
        <div class="child"></div>
        <div class="child"></div>
      </div>
    </section>
  </body>
</html>
```

<img :src="$withBase('/frontend/css/imgs/BFC-2.png')" alt="BFC-2.png">

#### BFC 会阻止外边距合并

**问题案例：外边距塌陷**

创建新的 BFC 避免两个相邻 div 之间的 外边距合并 问题

两个 p 中间取了最大值 100 为重叠了.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title></title>
  </head>
  <body>
    <section>
      <style>
        .top {
          height: 100px;
          margin-bottom: 50px;
          background-color: red;
        }

        .bottom {
          height: 100px;
          margin-top: 100px;
          background-color: blue;
        }
      </style>
      <p class="top"></p>
      <p class="bottom"></p>
    </section>
  </body>
</html>
```

<img :src="$withBase('/frontend/css/imgs/BFC-3-0.png')" alt="BFC-3-0.png">

在 p 外面包裹一层容器，并触发该容器生成一个 BFC。那么两个 P 便不属于同一个 BFC，就不会发生 margin 重叠了.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title></title>
  </head>
  <body>
    <section>
      <style>
        .wrap {
          overflow: hidden;
        }

        .top {
          height: 100px;
          margin-bottom: 50px;
          background-color: red;
        }

        .bottom {
          height: 100px;
          margin-top: 100px;
          background-color: blue;
        }
      </style>
      <p class="top"></p>
      <div class="wrap">
        <p class="bottom"></p>
      </div>
    </section>
  </body>
</html>
```

<img :src="$withBase('/frontend/css/imgs/BFC-3.png')" alt="BFC-3.png">

#### 应用-自适应两栏布局

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title></title>
  </head>
  <body>
    <section>
      <style>
        .left {
          width: 100px;
          float: left;
          height: 100px;
          background-color: yellow;
        }

        .right {
          height: 150px;
          background-color: red;
          overflow: hidden;
        }
      </style>
      <div class="left"></div>
      <div class="right"></div>
    </section>
  </body>
</html>
```

## display

### display 各值解析

| value        | describe                                                           |
| ------------ | ------------------------------------------------------------------ |
| none         | 元素会被隐藏，不显示                                               |
| inline       | 元素会被设置为内联元素，内部按行从左向右排列（元素前后没有换行符） |
| block        | 元素会被设置为块级元素，内部按列从上向下排列（元素前后带有换行符） |
| inline-block | 元素会被设置为行内块级元素，不会独占一行的块级元素                 |
| list-item    | 元素会作为列表显示                                                 |
| table        | 元素会作为块级表格来显示（类似 table），表格前后带有换行符         |
| flex         | 元素会进入 flex 布局模式                                           |

### inline、block、inline-block 三者区别

#### block

块级元素特点：

1. 每个块级元素都从新的一行开始，并且其后的元素也另起一行。（一个块级元素独占一行）
2. 元素的高度、宽度、行高以及顶和底边距都可设置。
3. 元素宽度在不设置的情况下，是它本身父容器的 100%（和父元素的宽度一致），除非设定一个宽度。

#### inline

内联元素特点：

1. 和其他元素都在一行上；
2. 元素的高度、宽度及顶部和底部边距不可设置；
3. 元素的宽度就是它包含的文字或图片的宽度，不可改变。

#### inline-block

- 内联块状元素（inline-block）就是同时具备内联元素、块状元素的特点。
  inline-block 元素特点：

1. 和其他元素都在一行上；
2. 元素的高度、宽度、行高以及顶和底边距都可设置。

#### 使用 display:inline-block 会产生的问题

- 问题--两个 display:inline-block 元素放到一起时会产生一段空白。
- 原因--元素被当成了行内元素排版的时候，元素之间的空白符（空格、回车换行等）都会被浏览器处理，根据 CSS 中 white-space 属性默认是 normal(合并多余空白），原来 HTML 代码中的回车换行符被转换成一个空白符，在字体不为 0 的情况下，空白符占据一定宽度，所以 inline-block 的元素之间就会出现空白间隙
- 解决方式
  _ 将子元素标签的结束符和下一个标签的开始符写在同一行
  _ 父元素中设置 font-size:0, 在子元素上设置正确 font-size \* 为子元素设置 float:left

## position

position 属性是用四种定位。默认的是 static。

- position:absolute（绝对定位） ——是脱离文档流，相对于父级元素（包含这个 position:relative）定位，当然如果没有，那就是相对于 body 定位的。
- position:relative（相对定位） ——单独使用，我不知道很多人是不是也跟我一样忽略过它，relative 也是不脱离文档流，“这个元素会偏移某个距离。但是该元素仍保持其未定位前的形状，它原本所占的空间仍保留。”，它是相对于自己来定位的，例如：#main{position:relative;top:-50px;},这时#main 会在相对于它原来的位置上移 50px。
- position:fixed（固定定位） —— 跟绝对定位有点类似，只是它的父级元素永远都是视窗本身。

---

- static（静态定位）
  对象遵循标准文档流中，top, right, bottom, left 等属性失效。
- relative（相对定位）
  对象遵循标准文档流中，依赖 top, right, bottom, left 等属性相对于该对象在标准文档流中的位置进行偏移，同时可通过 z-index 定义层叠关系。
- position:relative（相对定位） ——单独使用，我不知道很多人是不是也跟我一样忽略过它，relative 也是不脱离文档流，“这个元素会偏移某个距离。但是该元素仍保持其未定位前的形状，它原本所占的空间仍保留。”，它是相对于自己来定位的，例如：#main{position:relative;top:-50px;},这时#main 会在相对于它原来的位置上移 50px。
- absolute（绝对定位）
  对象脱离标准文档流，使用 top, right, bottom, left 等属性进行绝对定位（相对于 static 定位以外的第一个父元素进行绝对定位） 同时可通过 z-index 定义层叠关系。
- fixed（固定定位）
  对象脱离标准文档流，使用 top, right, bottom, left 等属性进行绝对定位（相对于浏览器窗口进行绝对定位）同时可通过 z-index 定义层叠关系。

补充--标准文档流

- 标准文档流指在不使用其他与排列和定位相关的特殊 CSS 规则时，元素的默认排列规则。
- HTML 文档中的元素可以分为两大类：行内元素和块级元素。
  - 行内元素，是 DOM 树中的一个节点。不占据单独的空间，依附于块级元素，行内元素没有自己的区域。
  - 块级元素，是 DOM 树中的一个节点。总是以块的形式表现出来，并且跟同级的兄弟块依次竖直排列，左右自动伸展，直到包含它的元素的边界，在水平方向不能并排。

## CSS3 新特性

1. 颜色：新增 RGBA，HSLA 模式
2. 文字阴影（text-shadow、）
3. 边框： 圆角（border-radius）边框阴影： box-shadow
4. 盒子模型：box-sizing
5. 背景：

- background-size 设置背景图片的尺寸 background-origin 设置背景图片的原点
- background-clip 设置背景图片的裁切区域，以”，”分隔可以设置多背景，用于自适应布局

6. 渐变：

- linear-gradient 线性渐变
- radial-gradient 径向渐变

7. 过渡：transition，可实现动画
8. 自定义动画 @keyframes animation
9. 在 CSS3 中唯一引入的伪元素是 ::selection.
10. 媒体查询，多栏布局
11. border-image
12. 2D 转换：transform：translate(x，y) rotate(x，y) skew(x，y) scale(x，y)
13. 3D 转换

---

css3 新增属性：

1. 边框

- border-radius 圆角边框
- box-shadow 边框阴影
- border-image 边框图片

2. 文本

- text-shadow 文本阴影

3. 2D

- transform：translate scale rotate skew

4. 3D

- translate：rotateX rotateY

5. 多背景 rgba
6. 线性渐变 gradient
7. 媒体查询
8. 多栏布局

::: tip

- CSS3 的特性那么多该从哪里说起了？很显然这道题目是有陷阱的，你不可能将所有的特性一个不漏的说出来，就算你说出来，别人还认为你是背的了！
- 所以你主要讲一下在项目中经常用到的 CSS3 的属性就可以，以第一人称来回答这个问题，例如：在我们的项目中经常用 CSS3 中的 XX 属性来实现 XX 特效。

项目中用到的：

- border-radius 圆角边框
- box-shadow 边框阴影
- transform
- animation
- width: fit-content
  - 补充：width 的一些属性

:::

### CSS3 新增伪类

- p:first-of-type 选择属于其父元素的首个 \<p\> 元素的每个 \<p\> 元素。
- p:last-of-type   选择属于其父元素的最后 \<p\> 元素的每个 \<p\> 元素。
- p:only-of-type   选择属于其父元素唯一的 \<p\> 元素的每个 \<p\> 元素。
- p:only-child    选择属于其父元素的唯一子元素的每个 \<p\> 元素。
- p:nth-child(2)   选择属于其父元素的第二个子元素的每个 \<p\> 元素。
- :enabled、:disabled 控制表单控件的禁用状态。
- :checked，单选框或复选框被选中。

## px、em、rem 的区别

在 css 中单位长度用的最多的是 px、em、rem，这三个的区别是：

- px 像素（Pixel）。相对长度单位。像素 px 是相对于显示器屏幕分辨率而言的。
- em（font size of the element）是指相对于父元素的字体大小的单位。这样就会存在一个问题，进行任何元素设置，都有可能需要知道他父元素的大小。
- rem（font size of the root element）是指相对于根元素（根元素 html）的字体大小的单位。这样就意味着，我们只需要在根元素确定一个参考值。
- 默认情况下 `16px = 1em = 1 rem`
  [字体大小之 px、em、rem、pt,字号详解](https://www.cnblogs.com/zhaowy/p/8400271.html)
