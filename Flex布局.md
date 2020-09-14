# Flex布局

## 目录

[对父级元素设置的属性](#jump1)

[对子级元素设置的属性](#jump2)

[几种常见布局的flex实现思路](#jump3)

---	

<span id="jump1"></span>

## 对父级元素设置的属性

### flex-direction:

设置主轴方向
	
属性值:

- row：默认值，从左到右

- row-reverse：从右到左

- column：从上到下

- column-reverse：从下到上

### justify-content

设置主轴上的子元素排列方式
	
注意，使用这个属性之前一定要确定主轴是哪个

属性值:

- flex-start：默认值，从头部开始。如果主轴是x轴，则从左到右

- flex-end：从尾部开始

- center：在主轴居中对齐。如果主轴是x轴则水平居中

- space-around：平分剩余空间

- space-between：先两边贴边，再平分剩余空间

### flex-wrap

设置子元素是否换行

属性值:

- nowrap：默认值，不换行

- wrap：换行

### align-items

设置侧轴上的子元素的排列方式（单行/列）

属性值:

- flex-start：默认值，如果侧轴是y轴，则从上到下

- flex-end：如果侧轴是y轴，则从下到上

- center：如果侧轴是y轴，则挤在一起居中（垂直居中）

- stretch：拉伸

### align-content

设置侧轴上的子元素的排列方式（多行/列），在单行下是没效果的
	
多行/列的定义：子元素不完全分布在x或y方向上的一行内

属性值：

- flex-start：默认值，如果侧轴是y轴，则从上到下

- flex-end：如果侧轴是y轴，则从下到上

- center：如果侧轴是y轴，则挤在一起居中（垂直居中）

- space-around：子元素在侧轴平分剩余空间

- space-between：子元素在侧轴先分布在两头，再平分剩余空间

- stretch：拉伸

### flex-flow

复合属性，相当于同时设置了flex-direction和flex-wrap


---

<span id="jump2"></span>

## 对子级元素设置的属性

### flex

flex属性定义子元素分配剩余空间，用flex来表示子元素占多少份数

```
.子元素类名 {
  flex:份数或百分比;
}
```

父元素会对所有的份数求和得到总份数，这样每个子元素的份数除以总份数就是它所占的比例

### align-self

控制子元素自己在侧轴上的排列方式

属性值和align-content差不多

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
