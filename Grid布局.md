# Grid布局

## 目录

[grid-template-columns、grid-template-rows](#jump1)

[repeat](#jump2)

[auto-fill关键字](#jump3)

[fr关键字](#jump4)

[gap](#jump5)

[grid-auto-flow](#jump6)

[justify-items、align-items](#jump7)

[justify-content、align-content](#jump8)

[grid-column-start、grid-column-end、grid-row-start、grid-row-end](#jump9)

[grid-area](#jump10)

[justify-self、align-self](#jump11)

---	

<span id="jump1"></span>

## grid-template-columns、grid-template-rows

### 基本语法

grid-template-columns属性定义每一列的列宽，grid-template-rows属性定义每一行的行高

```javascript
.container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px 100px;
}
```

上面的代码指定了一个三行三列的网格，列宽和行高都是100px

### 除了使用绝对单位，也可以使用百分比

```javascript
.container {
  display: grid;
  grid-template-columns: 33.33% 33.33% 33.33%;
  grid-template-rows: 33.33% 33.33% 33.33%;
}
```

### 网格线的名称

可以使用方括号，指定每一根网格线的名字，方便以后的引用

```javascript
.container {
  display: grid;
  grid-template-columns: [c1] 100px [c2] 100px [c3] auto [c4];
  grid-template-rows: [r1] 100px [r2] 100px [r3] auto [r4];
}
```

上面代码指定网格布局为3行 x 3列，因此有4根垂直网格线和4根水平网格线。方括号里面依次是这八根线的名字

网格布局允许同一根线有多个名字，比如[fifth-line row-5]

---

<span id="jump2"></span>

## repeat

### 可以使用repeat()函数，简化重复的值

repeat()接受两个参数，第一个参数是重复的次数，第二个参数是所要重复的值

例如：

```javascript
.container {
  display: grid;
  grid-template-columns: 33.33% 33.33% 33.33%;
  grid-template-rows: 33.33% 33.33% 33.33%;
}
```

可简化为：

```javascript
.container {
  display: grid;
  grid-template-columns: repeat(3, 33.33%);
  grid-template-rows: repeat(3, 33.33%);
}
```

### repeat()重复某种模式也是可以的

```javascript
grid-template-columns: repeat(2, 100px 20px 80px);
```

上面代码定义了6列，第一列和第四列的宽度为100px，第二列和第五列为20px，第三列和第六列为80px

---

<span id="jump3"></span>

## auto-fill 关键字

有时，单元格的大小是固定的，但是容器的大小不确定

如果希望每一行（或每一列）容纳尽可能多的单元格，这时可以使用auto-fill关键字表示自动填充

```javascript
.container {
  display: grid;
  grid-template-columns: repeat(auto-fill, 100px);
}
```

上面代码表示每列宽度100px，然后自动填充，直到容器不能放置更多的列

---

<span id="jump4"></span>

## fr 关键字

### 表示比例关系

网格布局提供了fr关键字（fraction 的缩写，意为"片段"）

如果两列的宽度分别为1fr和2fr，就表示后者是前者的两倍

```javascript
.container {
  display: grid;
  grid-template-columns: 1fr 1fr;
}
```

上面代码表示两个相同宽度的列

### fr可以与绝对长度的单位结合使用

```javascript
.container {
  display: grid;
  grid-template-columns: 150px 1fr 2fr;
}
```

上面代码表示，第一列的宽度为150像素，第二列的宽度是第三列的一半

---

<span id="jump5"></span>

## gap

row-gap属性设置行与行的间隔（行间距），column-gap属性设置列与列的间隔（列间距）

```javascript
.container {
  row-gap: 20px;
  column-gap: 20px;
}
```

gap属性是column-gap和row-gap的合并简写形式，语法如下：

```javascript
gap: <row-gap> <column-gap>;
```

---

<span id="jump6"></span>

## grid-auto-flow

### row和column

容器的子元素会按照grid-auto-flow属性，自动放置在每一个网格

默认的值是row，放置顺序是"先行后列"

也可以将它设成column，变成"先列后行"

### dense

grid-auto-flow属性除了设置成row和column，还可以设成row dense和column dense

布局会尽可能紧密填满，尽量不出现空格

---

<span id="jump7"></span>

## justify-items、align-items

### 基本语法

justify-items属性设置单元格内容的水平位置（左中右）

align-items属性设置单元格内容的垂直位置（上中下）

```javascript
.container {
  justify-items: start | end | center | stretch;
  align-items: start | end | center | stretch;
}
```

```javascript
start：对齐单元格的起始边缘。
end：对齐单元格的结束边缘。
center：单元格内部居中。
stretch：拉伸，占满单元格的整个宽度（默认值）。
```

### place-items

是align-items属性和justify-items属性的合并简写形式

```javascript
place-items: <align-items> <justify-items>;
```

---

<span id="jump8"></span>

## justify-content、align-content

### 基本语法

justify-content属性是整个内容区域在容器里面的水平位置（左中右）

align-content属性是整个内容区域的垂直位置（上中下）。

```javascript
.container {
  justify-content: start | end | center | stretch | space-around | space-between | space-evenly;
  align-content: start | end | center | stretch | space-around | space-between | space-evenly;  
}
```

```
start - 对齐容器的起始边框。
end - 对齐容器的结束边框。
center - 容器内部居中。
stretch - 项目大小没有指定时，拉伸占据整个网格容器。
space-around - 每个项目两侧的间隔相等。所以，项目之间的间隔比项目与容器边框的间隔大一倍。
space-between - 项目与项目的间隔相等，项目与容器边框之间没有间隔。
space-evenly - 项目与项目的间隔相等，项目与容器边框之间也是同样长度的间隔。
```

### place-content

是align-content属性和justify-content属性的合并简写形式

```javascript
place-content: <align-content> <justify-content>
```

---

<span id="jump9"></span>

## grid-column-start、grid-column-end、grid-row-start、grid-row-end

### 基本语法

项目的位置是可以指定的，具体方法就是指定项目的四个边框，分别定位在哪根网格线

```
grid-column-start属性：左边框所在的垂直网格线
grid-column-end属性：右边框所在的垂直网格线
grid-row-start属性：上边框所在的水平网格线
grid-row-end属性：下边框所在的水平网格线
```

```javascript
.item-1 {
  grid-column-start: 1;
  grid-column-end: 3;
  grid-row-start: 2;
  grid-row-end: 4;
}
```

### span

这四个属性的值还可以使用span关键字，表示"跨越"，即左右边框（上下边框）之间跨越多少个网格

```javascript
.item-1 {
  grid-column-start: span 2;
}
```

上面代码表示，1号项目的左边框距离右边框跨越2个网格

这与下面的代码效果完全一样

```javascript
.item-1 {
  grid-column-end: span 2;
}
```

### grid-column、grid-row

grid-column属性是grid-column-start和grid-column-end的合并简写形式，grid-row属性是grid-row-start属性和grid-row-end的合并简写形式

```javascript
.item {
  grid-column: <start-line> / <end-line>;
  grid-row: <start-line> / <end-line>;
}
```

---

<span id="jump10"></span>

## grid-area

grid-area属性指定项目放在哪一个区域

```javascript
.item-1 {
  grid-area: e;
}
```

---

<span id="jump11"></span>

## justify-self、align-self

### 基本语法

justify-self属性设置单元格内容的水平位置（左中右），跟justify-items属性的用法完全一致，但只作用于单个项目。

align-self属性设置单元格内容的垂直位置（上中下），跟align-items属性的用法完全一致，也是只作用于单个项目

```javascript
.item {
  justify-self: start | end | center | stretch;
  align-self: start | end | center | stretch;
}
```

### place-self

place-self属性是align-self属性和justify-self属性的合并简写形式

```javascript
place-self: <align-self> <justify-self>;
```
