# Rem布局

## 目录

[媒体查询](#jump1)

[less](#jump2)

[Rem布局](#jump3)

[](#jump)

[](#jump)

[](#jump)

---	

<span id="jump1"></span>

## 媒体查询

主要用来检测当前屏幕的大小

### 语法规范

```javascript
@media mediatype and|not|only (media feature) {
  CSS-Code;
}
```

### mediatype查询类型

all：用于所有设备

print：用于打印机打印预览

screen：用于电脑屏幕，平板电脑，智能手机等

### 关键字

and：可以将多个媒体特性连接到一起

not：排除某个媒体特性，可以省略

only：指定某个特定的媒体类型

### 媒体特性

width：定义输出设备中页面可见区域的宽度

min-width：定义输出设备中页面最小可见区域宽度

max-width：定义输出设备中页面最大可见区域宽度

在不同宽度变成不同颜色的效果：宽度从小写到大，则只需要写min-width不需要max-width，原理的样式层叠性

---

<span id="jump2"></span>

## less

### less嵌套

子元素的样式直接写到父元素里

内层选择器的前面没有&符号，则它被解析为父选择器的的后代

如果有&符号，则它被解析为：交集|伪类|伪元素选择器

### less运算

1. 运算符左右两侧必须加空格

2. 两个数参与运算，如果只有一个有单位，则以这个单位为准

3. 两个数参与运算，如果两者的单位不同，则以第一个单位为准

---

<span id="jump3"></span>

## Rem布局

1. 将屏幕划分为N等份

2. 将屏幕宽度除以N，得到html的字体大小baseFontSize

3. 设置宽度（或高度）为Apx元素的大小时，令其等于：Arem / baseFontSize
