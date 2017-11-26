# 多栏式布局

多栏式布局是 CSS 原生提供的一种内容分栏显示的解决方案。

## 基本用法

`column-count`属性指定`div`的子元素分成四栏。

```css
div {
  column-count:4;
}
```

`column-width`属性指定每一栏的宽度。

```css
div {
  column-width:100px;
}
```

上面代码中，`column-width`属性指定每一栏的宽度是100像素。如果`div`元素的宽度是800像素，那么内容就将分成8栏。

注意，`column-count`与`column-width`不应同时使用，它们之中同时只能有一个属性生效。另外，设定`position: fixed`和`position: absolute`子元素，将不纳入多栏式布局的栏计算。

## 间隔

多栏式布局对栏与栏之间的间隔，提供了如下属性。

- column-gap：间隔宽度
- column-rule-color：间隔线的颜色
- column-rule-style：间隔线的样式，比如`dashed`、`dotted`等，默认是`solid`
- column-rule-width：间隔线本身的宽度
- column-rule：`column-rule-color`、`column-rule-style`、`column-rule-width`这三个属性的快捷形式。

```css
div {
	column-gap: 20px;
	column-rule: 2px solid #33c;
}
```

上面代码指定栏与栏之间的间隔是`20px`，间隔线的样式是`2px solid #33c`。

## column-span

`column-span`属性指定某个子元素可以占据多栏的宽度，比如标题。它只能设两个值`all`和`none`。

```css
h2 {
  column-span: all;
}
```

## column-fill

`column-fill`属性指定内容如何在多栏之间分配。

默认值`balance`表示栏与栏是等高的，`auto`表示只占据内容所需的空间。

## 内容的断点

浏览器会自己决定，内容在栏与栏之间如何断点。下面的三个属性可以调整这个行为。

`break-inside`属性决定子元素内部如何断点。它可以取以下值。

- auto：默认值，表示子元素内部可以插入断点
- avoid：避免在子元素内部插入所有类型（page、column、region）的断点
- avoid-column：避免子元素内部插入栏与栏的断点

`break-before`属性决定子元素前方如何断点。它可以取以下值。

- auto：默认值，子元素前方可以插入断点
- avoid：避免在子元素前方插入所有类型（page、column、region）的断点
- avoid-column：避免在子元素前方插入栏与栏的断点
- column：子元素前方强制插入一个栏断点

`break-after`属性决定子元素后方如何断点。它可以取以下值。

- auto：默认值，子元素后方可以插入断点
- avoid：避免在子元素后方插入所有类型（page、column、region）的断点
- avoid-column：避免在子元素后方插入栏与栏的断点
- column：子元素后方强制插入一个栏断点

## 参考链接

- Molly E. Holzschlag, [CSS3 Multi-Column Layout](https://dev.opera.com/articles/css3-multi-column-layout/)
