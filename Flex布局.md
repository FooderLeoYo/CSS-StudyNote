# Flex布局

## 目录

[对父级元素设置的属性](#jump1)

[对子级元素设置的属性](#jump2)

[几种常见布局的flex实现思路](#jump3)

[特性](#jump4)

---	

<span id="jump1"></span>

## 对父级元素设置的属性

### justify-content

设置主轴上的子元素排列方式
	
注意，使用这个属性之前一定要确定主轴是哪个

属性值:

- flex-start：默认值，从头部开始。如果主轴是x轴，则从左到右

- flex-end：从尾部开始

- center：在主轴居中对齐。如果主轴是x轴则水平居中

- space-between：元素贴边，间隔相等

- space-around：两边留间隔，除两边外，其余间隔相等，两边间隔为其余间隔的一半

- space-evenly：两边留间隔，间隔相等

各属性效果如下图：

![](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/Flex/justfiy-content.png)

### align-items

设置侧轴上的子元素的排列方式（单行/列）

属性值:

- flex-start：默认值，如果侧轴是y轴，则从上到下

- flex-end：如果侧轴是y轴，则从下到上

- center：如果侧轴是y轴，则挤在一起居中（垂直居中）

- stretch：拉伸

- baseline/first baseline/last baseline：沿基线对齐

各属性效果如下图：

![](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/Flex/align-items.png)

### align-content

设置侧轴上的子元素的排列方式（多行/列），在单行下是没效果的
	
多行/列的定义：子元素不完全分布在x或y方向上的一行内

属性值：

- flex-start：默认值，如果侧轴是y轴，则从上到下

- flex-end：如果侧轴是y轴，则从下到上

- center：如果侧轴是y轴，则挤在一起居中（垂直居中）

- space-between：元素贴边，间隔相等

- space-around：两边留间隔，除两边外，其余间隔相等，两边间隔为其余间隔的一半

- space-evenly：两边留间隔，间隔相等

- stretch：拉伸

各属性效果如下图：

![](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/Flex/align-content.png)

### flex-direction:

设置主轴方向
	
属性值:

- row：默认值，从左到右

- row-reverse：从右到左

- column：从上到下

- column-reverse：从下到上

### flex-wrap

设置子元素是否换行

属性值:

- nowrap：默认值，不换行

- wrap：换行

- wrap-reverse：换行，第一行在下方

### flex-flow

复合属性，相当于同时设置了flex-direction和flex-wrap

---

<span id="jump2"></span>

## 对子级元素设置的属性

### lex-grow

flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大

如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍

### flex-shrink

flex-shrink属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小

如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小

### flex-basis

flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小

它可以设为一个具体的值（比如350px），则项目将固定占据350px的空间

### flex

flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选

建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值

用flex来表示子元素占多少份数：

```
.子元素类名 {
  flex:份数或百分比;
}
```

父元素会对所有的份数求和得到总份数，这样每个子元素的份数除以总份数就是它所占的比例

### align-self

align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性

默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch

该属性可能取6个值，除了auto，其他都与align-items属性完全一致

### order

定义子元素的排列顺序

数值越小，排列越靠前，默认为0

---

<span id="jump3"></span>

## 几种常见布局的flex实现思路

### 左右两边各放一个，中间自适应
步骤：

1. 父盒子设置  display: flex;

2. 左右两边的盒子给定width

3. 中间的盒子设置  flex: 1;

### 大盒子中的两个小盒子上下分布，水平居中

步骤：

1. 启用flex：父盒子设置  display: flex; 

2. 把主轴变为y轴：父盒子设置  flex-direction: column;

3. 侧轴（水平方向）设置居中对齐：父盒子设置  align-items: center; （或多行时align-content）
	
### 多个子项目之间等间距排列

#### 解决方案一

设置：

```
justify-content: space-evenly
```

#### 解决方案二

利用伪元素
		
html

```
<div class="list"> 
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
</div>
```

css

```
.list {
    width: 100%;
    height: 200px;
    background: #000;
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.item {
    width: 100px;
    height: 100px;
    background: red;
}
.list:before {
    content: "";
    display: block;
}
.list:after {
    content: "";
    display: block;
}
```

---

<span id="jump4"></span>

## 特性

设置flex后：

- 浮动失效

- 父容器margin不再与子元素margin重叠
