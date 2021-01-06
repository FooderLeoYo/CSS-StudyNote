# BFC

## 目录

[概念](#jump1)

[什么时候会生成BFC](#jump2)

[BFC具有的性质](#jump3)

[BFC的作用](#jump4)

[BFC、IFC、GFC 和 FFC](#jump5)

[](#jump)

---	

<span id="jump1"></span>

## 概念

BFC(Block formatting context)直译为"块级格式化上下文"

它是一个独立的渲染区域，只有 Block-level box 参与， 它规定了内部的 Block-level Box 如何布局，并且与这个区域外部毫不相干

---

<span id="jump2"></span>

## 什么时候会生成BFC

核心原理是：脱离文档流就会产生BFC

满足下列的任意一个或多个条件即可：

- 根元素，即 HTML 元素（最大的一个 BFC）

- float 的值不为 none

- position 的值为 absolute 或 fixed

- overflow 的值不为 visible（默认值。内容不会被修剪，会呈现在元素框之外）

- display 的值为 inline-block、table-cell、table-caption

---

<span id="jump3"></span>

## BFC具有的性质

- 内部的块元素会在垂直方向，一个接一个地放置。

- 块元素垂直方向的距离由margin决定。两个相邻块元素的垂直方向的margin会发生重叠。

- 每个元素的左外边距，与包含块的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此

- BFC的区域不会与float元素的区域重叠。

- BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。

- 计算BFC的高度时，浮动元素也参与计算

---

<span id="jump4"></span>

## BFC的作用

- 利用 BFC 避免外边距折叠

- 清除内部浮动 （撑开高度）

- 原理: 触发父 div 的 BFC 属性，使下面的子 div 都处在父 div 的同一个 BFC 区域之内

- 避免文字环绕

- 分属于不同的 BFC 时，可以阻止 margin 重叠

- 多列布局中使用 BFC

---

<span id="jump5"></span>

## BFC、IFC、GFC 和 FFC

- BFC（Block formatting contexts）：块级格式上下文

- IFC（Inline formatting contexts）：内联格式上下文

- GFC（GrideLayout formatting contexts）：网格布局格式化上下文

- FFC（Flex formatting contexts）:自适应格式上下文
