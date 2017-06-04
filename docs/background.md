# 背景

如果不定义背景图片或者背景色，一个网页元素的背景就是透明的。

## opaque

`opaque`的值在0到100之间。默认值是100，表示百分之百不透明，而0表示百分之百透明。

## background-attachment

`background-attachment`属性设置背景图案的位置，是否在视口里面是固定的，也就是说，是否随着滚动条一起滚动。由于存在两种滚动条——视口的滚动条和区块的滚动条——因此`background-attachment`的行为有三种模式，对应三个属性值。

- `scroll`：这个是默认值，表示背景图片绑定区块的内容，会随着视口滚动条滚动，但不会随着区块滚动条滚动。
- `fixed`：背景图片绑定视口，不会随着视口滚动条和区块滚动条滚动。
- `local`：背景图片会随着视口滚动条和区块滚动条滚动。

## background-repeat

`background-repeat`指定当背景图片小于容器时的平铺方式。

```css
html {
  background-image: url(logo.png);
  background-repeat: repeat-x;
}
```

它可以取以下值。

- repeat：背景图片沿容器的X轴和Y轴平铺，将会平铺满整个容器，可能会造成背景图片显示不全。
- repeat-x： 背景图片沿容器的X轴平铺。
- repeat-y：背景图片沿容器的Y轴平铺。
- no-repeat：背景图片不做任何平铺。
- round：背景图片沿容器的X轴和Y轴平铺，将会铺满整个容器。如果有多余空间，会升缩背景图片适应容器大小，不会造成图片显示不全。
- space：背景图片沿容器的X轴和Y轴平铺，将会铺满整个容器。如果有多余空间，不会改变背景图片的大小，而是平均分配相邻图片之间的空间，不会造成图片显示不全。

`background-repeat`可以设置两个值，分别表示 X 轴和 Y 轴的重复方式。

```css
.element {
/* background-repeat: horizontal vertical */
   background-repeat: repeat space;
   background-repeat: repeat repeat;
   background-repeat: round space;
}
```

`background-repeat`只设置一个值的时候，其实是下面方式的简写。

- `repeat`：相当于`repeat repeat`
- `repeat-x`：相当于`repeat-x no-repeat`
- `repeat-y`：相当于`no-repeat repeat`
- `no-repeat`：相当于`no-repeat no-repeat`
- `space`：相当于`space space`
- `round`：相当于`round round`

## 参考链接

- [单聊background-repeat](http://www.w3cplus.com/css3/css3-background-repeat-space-round.html)，by 大漠

