# 负margin及其应用

## 目录

[margin参考线](#jump1)

[margin-top为负值](#jump2)

[margin-left为负值](#jump3)

[margin-right为负值](#jump4)

[margin-bottom为负值](#jump5)

[margin负值的实际应用](#jump6)

---	

<span id="jump1"></span>

## margin参考线

参考线就是就是margin移动的基准点，而margin的值就是移动的数值

参考线不发生移动，移动的是margin；移动的结果为margin的宽度变化（margin为正值时）或非参考元素发生位移（margin为负值时）

margin的参考线有两类：一类是top、left，它们以外元素作为参考线；另一类是right、bottom，它们以自身作为参考线

下面这张图很直观地解释了margin的移动:

![magin移动规律](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/margin/magin%E7%A7%BB%E5%8A%A8%E8%A7%84%E5%BE%8B.jpg)

其中红色箭头表示margin为正值时的移动方向，当margin为负值的时候就反方向移动

---

<span id="jump2"></span>

## margin-top为负值

结构及样式：

```html
<div class="box">
     <div class="one">one</div>
    <div class="two">two</div>
</div>
<style>
.box {
    width:200px;
    height: 200px;
    border: 1px black solid;
}
.box div {
    width:100px;
    height: 100px;
}
.one {
	background:gray;
}
.two {
	background:orange;
	margin-top:-50px;
}
</style>
```

结果如下图：

![margin-top为负](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/margin/margin-top%E4%B8%BA%E8%B4%9F.png)

当设置div.two的margin-top为-50px的时候，它的参考线是div.one的下边。根据移动规则，这一设置使得div.two相对于参考线移动-50px，也即整个div.two向上移动50px

---

<span id="jump3"></span>

## margin-left为负值

结构及样式：

```html
<div class="box">
     <div class="one">one</div>
    <div class="two">two</div>
</div>
<style>
.box {
    width:200px;
    height: 200px;
    border: 1px black solid;
}
.box div {
    width:100px;
    height: 100px;
}
.one {
	background:gray;
	float: left;
}
.two {
	background:orange;
    margin-left: -50px;
    float: left;
}
</style>
```

结果如下图：

![margin-left为负](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/margin/margin-left%E4%B8%BA%E8%B4%9F.png)

---

<span id="jump4"></span>

## margin-right为负值

结构及样式：

```html
<div class="box">
     <div class="one">one</div>
    <div class="two">two</div>
</div>
<style>
.box {
    width:200px;
    height: 200px;
    border: 1px black solid;
}
.box div {
    width:100px;
    height: 100px;
}
.one {
    background:gray;
    float:left;
    margin-right:-50px;
}
.two {
    background:orange;
    float:left;
}
</style>
```

结果如下图：

![margin-right为负](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/margin/margin-right%E4%B8%BA%E8%B4%9F.png)

设置div.one的margin-right为-50px,这时候的参考线是div.one自身的右边界，因此div.one不动，div.two相对参考线移动-50px

---

<span id="jump5"></span>

## margin-bottom为负值

结构及样式：

```html
<div class="box">
     <div class="one">one</div>
    <div class="two">two</div>
</div>
<style>
.box {
    width:200px;
    height: 200px;
    border: 1px black solid;
}
.box div {
    width:100px;
    height: 100px;
}
.one {
    background:gray;
    margin-bottom:-50px;
}
.two {
    background:orange;
}
</style>
```

结果如下图：

![margin-bottom为负](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/margin/margin-bottom%E4%B8%BA%E8%B4%9F.png)

---

<span id="jump6"></span>

## margin负值的实际应用

### 边框去重

有的时候我们做Tab选项卡的时候不希望tab元素和父元素都加上边框，因此就可以给tab元素添加-1px的margin

### 左右布局

当margin设置为负值之后，不需要使用float也可以实现左右布局

结构及样式：

```html
<div class="container">
    <div class="left"></div>
    <div class="right"></div>
</div>
<style>
.container {
	width:400px;
	border: 1px solid black;
	padding:10px
}
.left {
	width: 100px;
	height:400px;
	background-color:gray;
}
.right {
	width: 300px;
	height:400px;
	margin:-400px 0 0 100px;
	background-color:orange;
}
</style>
```

结果如图：

![左右布局](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/margin/%E5%B7%A6%E5%8F%B3%E5%B8%83%E5%B1%80.jpg)

