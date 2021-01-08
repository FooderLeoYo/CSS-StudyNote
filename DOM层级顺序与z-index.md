# DOM层级顺序与z-index

## 目录

[顺序规则](#jump1)

[定位规则](#jump2)

[参与规则](#jump3)

[默认值规则](#jump4)

[从父规则](#jump5)

[层级树规则](#jump6)

[层叠上下文](#jump7)

[层叠的顺序表](#jump8)

---	

<span id="jump1"></span>

## 顺序规则

在不设置position属性（或设置成static）的情况下，文档流后面的DOM节点会覆盖前面的DOM节点

```html
<div id="a">A</div>
<div id="b">B</div>
```

![顺序规则](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/DOM%E5%B1%82%E7%BA%A7%E9%A1%BA%E5%BA%8F%E4%B8%8Ez-index/%E9%A1%BA%E5%BA%8F%E8%A7%84%E5%88%99.png)

---

<span id="jump2"></span>

## 定位规则

定位节点（position属性设置为relative，absolute或fixed的节点）会覆盖非定位节点（不设置position属性或position属性设为static的节点）

```html
<div id="a" style="position: relative">A</div>
<div id="b">B</div>
```

![定位规则](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/DOM%E5%B1%82%E7%BA%A7%E9%A1%BA%E5%BA%8F%E4%B8%8Ez-index/%E5%AE%9A%E4%BD%8D%E8%A7%84%E5%88%991.png)

根据顺序规则和定位规则, 我们可以做出更加复杂的结构。A和 B 都设为非定位节点，A 的子节点 A-1 设定定位节点

```javascript
<div id="a">
    <div id="a-1" style="position: relative">A</div>
</div>
<div id="b">B</div>
```

![更复杂的定位规则](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/DOM%E5%B1%82%E7%BA%A7%E9%A1%BA%E5%BA%8F%E4%B8%8Ez-index/%E5%AE%9A%E4%BD%8D%E8%A7%84%E5%88%992.png)

---

<span id="jump3"></span>

## 参与规则

z-index属性仅对定位节点生效

有三个DOM节点，其定位为static。但是A的z-index最大，但是依旧是在最底部，C的z-index最小，而在最顶部，因此可知z-index并未生效，此时为顺序规则在生效

```html
<div id="a" style="z-index: 2">A</div>
<div id="b" style="z-index: 1">B</div>
<div id="b" style="z-index: 0">C</div>
```

![参与规则](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/DOM%E5%B1%82%E7%BA%A7%E9%A1%BA%E5%BA%8F%E4%B8%8Ez-index/%E5%8F%82%E4%B8%8E%E8%A7%84%E5%88%991.png)

我们将B和C的position设置为relative之后，顺序发生了变化。根据参与者规则和定位规则，A不是定位节点，所以即使z-index最大，还是在最底部。而根据参与规则和默认值规则（下一节介绍），B和C都是定位节点，且B的z-index要大于C，所以B在最顶部

```html
<div id="a" style="z-index: 2">A</div>
<div id="b" style="position: relative; z-index: 1">B</div>
<div id="b" style="position: relative; z-index: 0">C</div>
```

![添加定位后](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/DOM%E5%B1%82%E7%BA%A7%E9%A1%BA%E5%BA%8F%E4%B8%8Ez-index/%E5%8F%82%E4%B8%8E%E8%A7%84%E5%88%992.png)

---

<span id="jump4"></span>

## 默认值规则

- 对于所有的定位节点，z-index值大的节点会覆盖z-index值小的节点

- z-index设为0和没有设置z-index的节点在同一层级内没有高低之分。在IE6和7种，z-index的默认值为0，其他浏览器中默认值为auto

```html
<div id="a" style="position: relative; z-index: 1">A</div>
<div id="b" style="position: relative; z-index: 0">B</div>
<div id="c" style="position: relative">C</div>
<div id="d" style="position: relative; z-index: 0">D</div>
```

![默认值规则](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/DOM%E5%B1%82%E7%BA%A7%E9%A1%BA%E5%BA%8F%E4%B8%8Ez-index/%E9%BB%98%E8%AE%A4%E5%80%BC%E8%A7%84%E5%88%99.png)

---

<span id="jump5"></span>

## 从父规则

两个节点A和B都是定位节点，如果节点A的z-index值比节点B的大，那么节点A的子元素都会覆盖在节点B以及节点B的子节点上

```html
<div id="a" style="position: relative; z-index: 1">
    <div id="a-1">A-1</div>
</div>
<div id="b" style="position: relative; z-index: 0">
    <div id="b-1">B-1</div>
</div>
```

![从父规则](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/DOM%E5%B1%82%E7%BA%A7%E9%A1%BA%E5%BA%8F%E4%B8%8Ez-index/%E4%BB%8E%E7%88%B6%E8%A7%84%E5%88%991.png)

如果定位节点A和B的z-index值一样大，那么根据顺序规则，B会覆盖A，那么即使A的子节点的z-index比B的子节点大，B的子节点还是会覆盖A的子节点。(这就是为什么即使我们把A-1的z-index设置得很大，依然无法盖住B节点的原因)

```html
<div id="a" style="position: relative; z-index: 0">
    <div id="a-1" style="position: relative; z-index: 2">A-1</div>
</div>
<div id="b" style="position: relative; z-index: 0">
    <div id="b-1" style="position: relative; z-index: 1">B-1</div>
</div>
```

![父盒子z-index一样大](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/DOM%E5%B1%82%E7%BA%A7%E9%A1%BA%E5%BA%8F%E4%B8%8Ez-index/%E4%BB%8E%E7%88%B6%E8%A7%84%E5%88%992.png)

---

<span id="jump6"></span>

## 层级树规则

定位节点，且z-index有整数值的（不包括z-index:auto），会被放置到一个与DOM节点不一样的层级树里

在下面的DOM节点中，A和B是兄弟节点，但是在层级树种，A和B-1才是兄弟节点（因为他们都是Root下的第一层含有整数z-index的定位节点），所以A在B和B-1之上。虽然A-1的z-index比B-1的小，但是根据从父规则，A-1也在B-1之上

```html
<div id="a" style="position: relative; z-index: 2">
    <div id="a-1" style="position: relative; z-index: 0">A-1</div>
</div>
<div id="b">
    <div id="b-1" style="position: relative; z-index: 1">B-1</div>
</div>
```

![层级树](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/DOM%E5%B1%82%E7%BA%A7%E9%A1%BA%E5%BA%8F%E4%B8%8Ez-index/%E5%B1%82%E7%BA%A7%E6%A0%91%E8%A7%84%E5%88%991.png)

![层级树规则](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/DOM%E5%B1%82%E7%BA%A7%E9%A1%BA%E5%BA%8F%E4%B8%8Ez-index/%E5%B1%82%E7%BA%A7%E6%A0%91%E8%A7%84%E5%88%992.png)

下面是一个更复杂的层级树

首先最外层的A、C有定位，因此它们在B之上；而A、C均无z-index，因此按顺序规则C在A之上

然后由于A、B、C均无z-index，因此它们没有创建出独立的层级树。所以即使最外层盒子的顺序是：C、A、B，它们的子元素也不会套用从父规则，而是按照各自的z-index大小来排序，因此顺序为：A-1、B-1-1、C-1-1-1

```html
<div id="a" style="position: relative">
    <div id="a-1" style="position: relative; z-index: 100">A-1</div>
</div>
<div id="b">
    <div id="b-1" style="position: relative">
        <div id="b-1-1" style="position: relative; z-index: 10">B-1-1</div>
    </div>
</div>
<div id="c" style="position: relative">
    <div id="c-1">
        <div id="c-1-1">
            <div id="c-1-1-1" style="position: relative; z-index: 1">C-1-1-1</div>
        </div>
    </div>
</div>
```

![更复杂的层级树](https://raw.githubusercontent.com/FooderLeoYo/CSS-StudyNote/master/assets/img/DOM%E5%B1%82%E7%BA%A7%E9%A1%BA%E5%BA%8F%E4%B8%8Ez-index/%E5%B1%82%E7%BA%A7%E6%A0%91%E8%A7%84%E5%88%993.png)

---

<span id="jump7"></span>

## 层叠上下文

### 概念

层叠上下文是HTML元素的三维概念，这些HTML元素在一条假想的相对于面向（电脑屏幕的）视窗或者网页的用户的z轴上延伸，HTML元素依据其自身属性按照优先级顺序占用层叠上下文的空间

### 特性

- 子元素的 z-index 值只在父级层叠上下文中有意义

- 子级层叠上下文被自动视为父级层叠上下文的一个独立单元

产生的条件

满足一下其中一个条件，即可产生一个层叠上下文：

- 根元素 (HTML),

- z-index 值不为 "auto"的 绝对/相对定位，

- position: fixed

- opacity 属性值小于 1 的元素

- transform 属性值不为 "none"的元素

- filter值不为“none”的元素

- -webkit-overflow-scrolling 属性被设置 "touch"的元素

---

<span id="jump8"></span>

## 层叠的顺序表

| 位置 | 描述 | CSS |
| --- | --- | --- |
| 1 | 包含该层叠上下文的父元素 |  |
| 2 | 负堆叠顺序的子元素 | ```	z-index: <negative integer>; position: relative (or absolute or fixed)``` |
| 3 | 文档流中，非内联，非定位子元素 | ```display: /* not inline */; position: static``` |
| 4 | 非定位浮动子元素 | ```	float: left (or right); position: static``` |
| 5 | 内联流，非定位子元素 | ```display: inline; position: static``` |
| 6 | 堆叠顺序为0的子元素 | ```	z-index: auto (or 0); position: position: relative(or absolute or fixed)``` |
| 7 | 堆叠顺序为正的子元素 | ```z-index: <positive integer>; position: relative(or absolute or fixed)``` |