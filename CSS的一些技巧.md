# CSS的一些技巧

## 目录

[字体图标](#jump1)

[三角形的制作](#jump2)

[CSS用户界面样式](#jump3)

[溢出文字以省略号显示](#jump4)

[圆角边框](#jump5)

[盒子阴影](#jump6)

[Emmet语法](#jump7)

[](#jump)

---	

<span id="jump1"></span>

## 字体图标

本质是字体

### 导入字体图标

以下步骤为阿里字体图标库的使用

1. 将目标字体图标加入购物车

2. 点击右上角购物车图标，点击添加到目标项目，自动跳转到项目页面

3. 赋值@font-face代码段，粘贴到全局css文件，或新建一个css文件后在需要用的地方导入它

4. 赋值目标图标的8位代码，在需要使用的标签中，添加class="iconfont"，在内容部分粘贴8位代码

### 追加字体图标

在Iconfont网站里点重新上传，选压缩包里的selection.json，里面记录了之前已选的图标

---

<span id="jump2"></span>

## 三角形的制作

### 三角的原理

一个宽、高都是0的盒子，如果指定边框，则会显示成四个三角形拼成的正方形

因此，想得到一个三角形可以，则可以隐藏其他三个：

```javascript
.box2 {
    width: 0;
    height: 0;
    border: 50px solid transparent;
    border-left-color: pink;
}
```

### 非等腰直角三角形

```javascript
.box1 {
    width: 0;
    height: 0;
    /* 1.只保留右边的边框有颜色 */
    border-color: transparent red transparent transparent;
    /* 2. 样式都是solid */
    border-style: solid;
    /* 3. 上边框宽度要大， 右边框 宽度稍小， 其余的边框该为 0 */
    border-width: 100px 50px 0 0;
}
```

---

<span id="jump3"></span>

## CSS用户界面样式

### 鼠标样式cursor:

属性值

- default 默认的小白鼠标

- pointer 鼠标小手

- move 移动十字架

- text 文本I

- not-allowed 禁止红圈斜杠

### 去掉表单默认的蓝色边框

```javascript
outline: none;
```

### 防止拖拽文本域resize

```javascript
resize: none;
```

---

<span id="jump4"></span>

## 溢出文字以省略号显示

### 单行文字

分三步：

```javascript
/* 1.这个单词的意思是如果文字显示不开也必须强制一行内显示 */
white-space: nowrap;
/* 2.溢出的部分隐藏起来 */
overflow: hidden;
/* 3. 文字溢出的时候用省略号来显示 */
text-overflow: ellipsis;
```

### 多行文字

```javascript
overflow: hidden;
text-overflow: ellipsis;
/* 弹性伸缩盒子模型显示 */
display: -webkit-box;
/* 限制在一个块元素显示的文本的行数 */
-webkit-line-clamp: 3;
/* 设置或检索伸缩盒对象的子元素的排列方式 */
-webkit-box-orient: vertical;
```

但是这个方法有兼容性问题，且后台操作起来更简单，因此多行加省略号一般是后台人员来做

---

<span id="jump5"></span>

## 圆角边框

### 简写语法

```javascript
border-radius: 数值px/百分比;
```

百分比是盒子宽度的百分比

### 完整写法

写一个值是简写，最多可以写4个值，分别控制左上角、右上角、右下角、左下角

写两个值：左上角右下角、右上角左下角

### 只改动一个角

```javascript
border-top-left-radius:
border-top-right-radius:
border-bottom-left-radius:
border-bottom-right-radius:
```

---

<span id="jump6"></span>

## 盒子阴影

```javascript
box-shadow: h-shadow v-shadow blur pread color inset;
```

h-shadow v-shadow必需，允许负值

---

<span id="jump6"></span>

## Emmet语法

使用Emmet语法，可以快速生成HTML结构语法

常用的Emmet语法包括：

- 标签名+tab：可生成一个标签

- 标签名*数字：可以生成多个标签

- 标签名.类名：生成带类的标签

- 标签名#id名：生成带id的标签

- >：生成父子关系的标签

- $*数字：生成一组自增序列

- 标签名{}：生成带内容的标签
