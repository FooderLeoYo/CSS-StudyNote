# 几种常见的 CSS 布局

## 目录

[常见布局](#jump1)

[单列布局](#jump2)

[两列自适应布局](#jump3)

[三栏布局](#jump4)

[等高布局](#jump5)

[粘连布局](#jump6)

[](#jump)

[](#jump)

[](#jump)

[](#jump)

---	

<span id="jump1"></span>

## 常见布局

![常见布局](https://github.com/FooderLeoYo/CSS-StudyNote/blob/master/assets/img/%E5%87%A0%E7%A7%8D%E5%B8%B8%E8%A7%81%E7%9A%84%20CSS%20%E5%B8%83%E5%B1%80/%E5%B8%B8%E8%A7%81%E5%B8%83%E5%B1%80%E6%80%9D%E7%BB%B4%E5%AF%BC%E5%9B%BE.webp.jpg?raw=true)

---

<span id="jump2"></span>

## 单列布局

### 分类

常见的单列布局有两种：

header,content和footer等宽的单列布局
header与footer等宽,content略窄的单列布局

![单列布局](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/%E5%87%A0%E7%A7%8D%E5%B8%B8%E8%A7%81%E7%9A%84%20CSS%20%E5%B8%83%E5%B1%80/%E5%8D%95%E5%88%97%E5%B8%83%E5%B1%80.jpg)

### 第一种的实现

先通过对header,content,footer统一设置width：1000px;或者max-width：1000px(这两者的区别是当屏幕小于1000px时，前者会出现滚动条，后者则不会，显示出实际宽度);

然后设置margin:auto实现居中即可得到

```html
<div class="header"></div>
<div class="content"></div>
<div class="footer"></div>
```

```css
.header{
    margin:0 auto; 
    max-width: 960px;
    height:100px;
    background-color: blue;
}
.content{
    margin: 0 auto;
    max-width: 960px;
    height: 400px;
    background-color: aquamarine;
}
.footer{
    margin: 0 auto;
    max-width: 960px;
    height: 100px;
    background-color: aqua;
}
```

### 第二种的实现

```html
<div class="header">
    <div class="nav"></div>
</div>
<div class="content"></div>
<div class="footer"></div>
```

```css
.header{
    margin:0 auto;
    max-width: 960px;
    height:100px;
    background-color: blue;
}
.nav{
    margin: 0 auto;
    max-width: 800px;
    background-color: darkgray;
    height: 50px;
}
.content{
    margin: 0 auto;
    max-width: 800px;
    height: 400px;
    background-color: aquamarine;
}
.footer{
    margin: 0 auto;
    max-width: 960px;
    height: 100px;
    background-color: aqua;
}
```

---

<span id="jump3"></span>

## 两列自适应布局

两列自适应布局是指一列由内容撑开，另一列撑满剩余宽度的布局方式

### float+overflow:hidden

这种办法主要通过overflow触发BFC，而BFC不会重叠浮动元素

由于设置overflow:hidden并不会触发IE6-浏览器的haslayout属性，所以需要设置zoom:1来兼容IE6-浏览器

结构及样式：

```html
<div class="parent" style="background-color: lightgrey;">
    <div class="left" style="background-color: lightblue;">
        <p>left</p>
    </div>
    <div class="right"  style="background-color: lightgreen;">
        <p>right</p>
        <p>right</p>
    </div>        
</div>
```

```css
.parent {
  overflow: hidden;
  zoom: 1;
}
.left {
  float: left;
  margin-right: 20px;
}
.right {
  overflow: hidden;
  zoom: 1;
}
```

### Flex布局

```css
//html部分同上
.parent {
  display:flex;
}  
.right {
  margin-left:20px; 
  flex:1;
}
```

### grid布局

```css
//html部分同上
.parent {
  display:grid;
  grid-template-columns:auto 1fr;
  grid-gap:20px
} 
```

---

<span id="jump4"></span>

## 三栏布局

特征：中间列自适应宽度，旁边两侧固定宽度

### 圣杯布局

#### 结构及样式

必须是先写center，这样才能保证center在left和right的“前面”

```html
  <article class="container">
    <div class="center">
      <h2>圣杯布局</h2>
    </div>
    <div class="left"></div>
    <div class="right"></div>
  </article>
```

```css
  .container {
    padding-left: 220px;//为左右栏腾出空间
    padding-right: 220px;
  }
  .left {
    float: left;
    width: 200px;
    height: 400px;
    background: red;
    margin-left: -100%;
    position: relative;
    left: -220px;
  }
  .center {
    float: left;
    width: 100%;
    height: 500px;
    background: yellow;
  }
  .right {
    float: left;
    width: 200px;
    height: 400px;
    background: blue;
    margin-left: -200px;
    position: relative;
    right: -220px;
  }
```

#### 实现步骤

- 三个部分都设定为左浮动，然后设置center的宽度为100%，由于html中center在前，因此center会先占满一行，left和right则会被挤到下一行

![圣杯布局](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/%E5%87%A0%E7%A7%8D%E5%B8%B8%E8%A7%81%E7%9A%84%20CSS%20%E5%B8%83%E5%B1%80/%E5%9C%A3%E6%9D%AF%E5%B8%83%E5%B1%801.webp.jpg)

- 通过设置margin-left为负值让left和right部分回到与center部分同一行

![](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/%E5%87%A0%E7%A7%8D%E5%B8%B8%E8%A7%81%E7%9A%84%20CSS%20%E5%B8%83%E5%B1%80/%E5%9C%A3%E6%9D%AF%E5%B8%83%E5%B1%802.webp.jpg)

- 通过设置父容器的padding-left和padding-right，让左右两边留出间隙

![](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/%E5%87%A0%E7%A7%8D%E5%B8%B8%E8%A7%81%E7%9A%84%20CSS%20%E5%B8%83%E5%B1%80/%E5%9C%A3%E6%9D%AF%E5%B8%83%E5%B1%803.webp.jpg)

- 通过设置相对定位，让left和right部分移动到两边的间隙

![](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/%E5%87%A0%E7%A7%8D%E5%B8%B8%E8%A7%81%E7%9A%84%20CSS%20%E5%B8%83%E5%B1%80/%E5%9C%A3%E6%9D%AF%E5%B8%83%E5%B1%804.webp.jpg)

### 双飞翼布局

#### 结构与样式

同样必须先写center

```html
<article class="container">
    <div class="center">
        <div class="inner">双飞翼布局</div>
    </div>
    <div class="left"></div>
    <div class="right"></div>
</article>
```

```css
.container {
    min-width: 600px;//确保中间内容可以显示出来，两倍left宽+right宽
}
.left {
    float: left;
    width: 200px;
    height: 400px;
    background: red;
    margin-left: -100%;
}
.center {
    float: left;
    width: 100%;
    height: 500px;
    background: yellow;
}
.center .inner {
    margin: 0 200px; //新增部分
}
.right {
    float: left;
    width: 200px;
    height: 400px;
    background: blue;
    margin-left: -200px;
}
```

#### 实现步骤

- 三个部分都设定为左浮动，然后设置center的宽度为100%，left和right部分会被挤到到下一行

- center部分增加一个内层div，不设宽度，设margin: 0 200px作为left和right的预留位

- 通过设置margin-left为不同的负值，让left和right部分回到与center部分同一行并正好落在预留位

#### 缺点

多加一层 dom 树节点，增加渲染树生成的计算量

---

<span id="jump5"></span>

## 等高布局

等高布局是指子元素在父元素中高度相等的布局方式

### 利用正padding+负margin

首先设置一个大数值的 padding-bottom，开辟预留位

然后再设置相同数值的负的 margin-bottom，将元素的下边界拉回来（不是把元素缩小回来）

最后在所有列外面加上一个容器，并设置 overflow:hidden，溢出剪切线为下边界也即margin-bottom，而不是包含大padding的元素的实际大小

例如，此方法便可解决圣杯布局的缺点，新增代码如下：

```css
.center,
.left,
.right {
  padding-bottom: 10000px;
  margin-bottom: -10000px;
}
.container {
  padding-left: 220px;
  padding-right: 220px;
  overflow: hidden; //把溢出背景切掉
}
```

### 利用背景图片

使用背景图片，在列的父元素上使用这个背景图进行Y轴的铺放，从而实现一种等高列的假象

在制作样式之前需要一张类似下面的背景图：

![](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/%E5%87%A0%E7%A7%8D%E5%B8%B8%E8%A7%81%E7%9A%84%20CSS%20%E5%B8%83%E5%B1%80/%E5%88%A9%E7%94%A8%E8%83%8C%E6%99%AF%E5%9B%BE%E7%89%87.jpg)

```html
<div class=”container clearfix”>
    <div class=”left”></div>
    <div  class=”content”></div>
    <div class=”right”></div>
</div>
```

```css
.container {
  background: url("column.png") repeat-y;
  width: 960px;
  margin: 0 auto;
}
.left {
  float: left;
  width: 220px;
}
.content {
  float: left;
  width: 480px;
}
.right {
  float: left;
  width: 220px;
}
```

---

<span id="jump6"></span>

## 粘连布局

### 特点

- 有一块内容```<main>```，当```<main>```的高康足够长的时候，紧跟在```<main>```后面的元素```<footer>```会跟在```<main>```元素的后面

- 当```<main>```元素比较短的时候(比如小于屏幕的高度),我们期望这个```<footer>```元素能够“粘连”在屏幕的底部

如下图：

![](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/%E5%87%A0%E7%A7%8D%E5%B8%B8%E8%A7%81%E7%9A%84%20CSS%20%E5%B8%83%E5%B1%80/%E7%B2%98%E8%BF%9E%E5%B8%83%E5%B1%80.webp.jpg)

### 结构与样式

```html
<div id="wrap">
  <div class="main">
    main <br />
    main <br />
    main <br />
  </div>
</div>
<div id="footer">footer</div>
```

```css
* {
    margin: 0;
    padding: 0;
  }
  html,
  body {
    height: 100%;//高度一层层继承下来
  }
  #wrap {
    min-height: 100%;
    background: pink;
    text-align: center;
    overflow: hidden;
  }
  #wrap .main {
    padding-bottom: 50px;
  }
  #footer {
    height: 50px;
    line-height: 50px;
    background: deeppink;
    text-align: center;
    margin-top: -50px;
  }
```

### 实现步骤

- footer必须是一个独立的结构，与wrap没有任何嵌套关系

- wrap区域的高度通过设置min-height，变为视口高度

- footer要使用margin为负来确定自己的位置

- 在main区域需要设置 padding-bottom。这也是为了防止负 margin 导致 footer 覆盖任何实际内容
