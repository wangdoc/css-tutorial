# 颜色

## 颜色关键字

CSS 允许使用关键字表示颜色，CSS2.1 设置了16个基本的颜色，CSS 3 又增加了131个。

## 六位颜色表示法

六位颜色表示法又称为 RGB 表示，分别使用两位十六进制数表示红色（R）、绿色（G）、蓝色（B），组合在一起就是六位，然后加上`#`前缀，比如`#59007F`。

每种颜色使用0～255表示浓度，0表示没有，255表示浓度最深。

如果一个十六进制颜色是由三对重复的数字组成的，如`#ff3344`，可以缩写为`#f34`。

## 八位颜色表示法

Chrome 浏览器支持八位的颜色表示法`RRGGBBAA`，前六位是红、绿、蓝颜色值，后两位表示透明度（alpha transparency）。比如，`#ffffff80`相当于`rgba(255, 255, 255, .5)`。

alpha设置越接近0，颜色就越透明。如果设为0，就是完全透明的，就像没有设置任何颜色。类似地，1表示完全不透明。

## HSL 和 HSLA 表示法

HSL 代表色相（hue）、饱和度（saturation）和亮度（lightness），其中色相的取值范围为0～360，饱和度和亮度的取值均为百分数，范围为0～100%。

- 红色为hsl(0,100%,50%);
- 黄色为hsl(60,100%,50%);
- 绿色为hsl(120,100%,50%);
- 青色为hsl(180,100%,50%);
- 蓝色为hsl(240,100%,50%);
- 紫红色为hsl(300,100%,50%);

用HSLA指定alpha透明度的方法与RGBA是一致的。

## currentColor

`currentColor`是一个属性值，代表当前元素的`color`属性的值。

```css
.box {
  color: red;
  border: 1px solid currentColor;
  box-shadow: 0 0 2px 2px currentColor;
}
```

上面代码，`border`和`box-shadow`的颜色都与`color`保持一致。这种写法的好处是，如果要修改`color`，只要修改一处就可以了，不用修改三个地方。

`currentColor`的另一个用处，是让衍生类都继承基类的颜色。

```css
.box {
    color: red;
}
.box .child-1 {
    background: currentColor;
}
.box .child-2 {
    color: currentColor;
    border 1px solid currentColor;
}
```

伪元素也可以使用`currentColor`。

```css
.box {
    color: red;
}
.box:before {
    color: currentColor;
    border: 1px solid currentColor;
}
```

## 参考链接

- [使用 currentColor 属性写出更好的 CSS 代码](http://www.qcyoung.com/2016/09/28/%E3%80%90%E8%AF%91%E3%80%91%E4%BD%BF%E7%94%A8%20currentColor%20%E5%B1%9E%E6%80%A7%E5%86%99%E5%87%BA%E6%9B%B4%E5%A5%BD%E7%9A%84%20CSS%20%E4%BB%A3%E7%A0%81/)
