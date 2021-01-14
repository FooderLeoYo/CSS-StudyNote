# 负margin及其应用

## 目录

[margin参考线](#jump1)

[对未脱标元素的影响](#jump2)

[对已脱标元素的影响](#jump3)

[对未设置width的元素的影响](#jump4)

[](#jump)

[](#jump)

---	

<span id="jump1"></span>

## margin参考线

参考线就是就是margin线移动的起点，而margin的值就是移动的数值

margin的参考线有两类：一类是top、left，它们以外元素作为参考线；另一类是right、bottom，它们以自身作为参考线。这么分类的根据是文档流只会向左和向上，不可能向右和向下，元素并不会如你所想的那样向右或下移动，而是将后续的元素拖拉进来，覆盖本来的元素

在文档流中，元素的最终边界是由margin决定的，margin为负的时候就相当于元素的边界向里收。文档流认的只是这个边界，不会管你实际的尺寸是多少，因此就会出现元素设置负margin后使得“后面的”元素移过来并叠在它上面的效果

下面这张图很直观地解释了margin的移动:

![magin移动规律](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/margin/magin%E7%A7%BB%E5%8A%A8%E8%A7%84%E5%BE%8B.jpg)

其中红色箭头表示margin为正值时margin线的移动方向，当margin为负值的时候就反方向移动

---

<span id="jump2"></span>

## 对未脱标元素的影响

### 规律

在标准流中，当margin为负时：

- margin-left 和 margin-top：影响自身元素，将向指定方向偏移

- margin-right 和 margin-bottom：影响“后面的”元素，将其拖入指定方向

### 演示

#### margin-top为负

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

当设置div.two的margin-top为-50px的时候，它的参考线是div.one的下边。根据移动规则，这一设置使得div.two的margin-top线相对于参考线向上移动50px，即此时div.one与div.two的边界向上移动了50px，结果就使得整个div.two向上移动50px

#### margin-right为负值

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

设置div.one的margin-right为-50px，这时候的参考线是div.one自身的右边界。根据规则，这一设置使得div.one的margin-right线相对于参考线向左移动50px，即此时div.one与div.two的边界向左移动了50px，结果就使得div.two相对参考线移动-50px

---

<span id="jump3"></span>

## 对已脱标元素的影响

### 对绝对定位元素的影响

当设置负值的 margin 的方向为 top 或者 left 的时候，元素的表现与未脱标前一样

当设置负值的 margin 的方向为 right/bottom 的时候，由于设置绝对定位的元素已经脱标，所以虽然负margin依然会使它的边界收缩，但后面的元素此时与它已不在同一个流中（位于下方），因此后面的元素并不会发生位移

### 对浮动元素的影响

### 左浮动时

当为左浮动时，与绝对定位时的情况一致

### 右浮动时

唯一的本质区别是参考线的变化

当为右浮动时，margin-right的参考线为右边前面元素（或父元素）的边，margin-left的参考线为浮动元素自己的左边

因此，margin-right为负时，浮动元素向右移动

margin-left为负时，浮动元素的边界向左收缩，但由于自身脱标，因此左边的标准流元素将不会发生位移

上下margin与绝对定位时的情况一致

---

<span id="jump4"></span>

## 对未设置width的元素的影响

这个作用能实现的前提是：该元素没有设定width属性（当然width:auto是可以的）

给一个无宽度的标准流元素设置margin-right为负值，会使该元素向右拓宽相应的值；设置margin-left同理

原理：没有设置 width 的元素的宽度值是由包围元素的宽度，减去 margin，来计算出来的，减去一个负值相当于加上它的正值，所以就会得到实际上比原始元素更宽的值
