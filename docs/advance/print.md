# 打印样式

## 基本用法

`@media print`命令可以设置打印样式，即用户选择打印当前网页时，生效的 CSS 规则。

```css
@media print {
  h1 { font-size: 16pt; }
}
```

上面代码设置的`h1`样式，对屏幕浏览不产生效果，只有用户打印网页时才会生效。

`@media print`命令可以与正常样式规则混合使用。

```css
p { margin: 1em 0; }

@media print {
  .related-articles { display: none; }
}
```

上面代码中，`p`元素的样式对屏幕浏览和打印都有效，`.related-articles`的样式只对打印有效。

如果要设置某些规则只对屏幕浏览有效，可以像下面这样写。

```css
@media screen {
  /* 只对屏幕浏览有效 */
}

@media print {
  /* 只对打印有效 */
}
```

## 分页符

分页符属性用来设置页面的分页（即另起一页），共有三个相关属性。

- page-break-before：元素之前分页
- page-break-after：元素之后分页
- page-break-inside：元素内部分页

这三个属性的值都是两个：`always`（生效）和`avoid`（避免）。

```css
h1 {
  /* 总是在 h1 元素之前分页 */
  page-break-before: always;
}

section.city-map {
  /* 在元素之前和之后分页，即该元素单独占据一页 */
  page-break-before: always;
  page-break-after: always;
}

table {
  /* 表格尽可能不要分页 */
  page-break-inside: avoid;
}
```

## orphans 属性，widow 属性

`orphans`属性和`widow`属性设置某个元素如何跨页拆分。

`orphans`属性设置跨页前的行数少于多少行时，所有行都移到下一页打印。

```css
p {
  orphans: 3;
}
```

上面代码设置，如果某个段落出现在上一页的结尾少于3行（比如只有两行），那么该段落全部移到下一页显示。

`widow`属性设置出现在新页面的行数，最少应该有几行。

```css
p {
  widow: 2;
}
```

上面代码设置，如果某个段落出现在新页面的开头少于两行（比如只有一行），那么该段落全部移到上一页显示。

## @page 命令

`@page`命令主要用来定义页面距。

```css
@page {
  margin: 2cm;
}
```

此外，还可以用`:first`、`:last`、`:left`、`:right`和`:blank`选择器，选中特殊页面。

```css
@page:first {
  margin: 0;
}
```

上面代码设置第一页的页边距为`0`。

## 技巧

### 重复表格的表头

如果希望打印表格的时候，每一页都出现表头，只需要使用`<thead>`元素定义表头，`<tbody>`元素定义表的数据部分即可。

```html
<table>
  <thead>
    <tr>
      <th>City</th>
      <th>Population</th>
  </thead>
  <tbody>
    <tr>
      <td>Sydney</td>
      <td>4.627 million (2018)</td>
    </tr>
  </tbody>
</table>
```

上面代码中，如果表格跨页，表头的`City`和`Population`字段会在每一页都打印出来。

### 打印链接的网址

如果希望打印出链接的网址，可以使用`:after`伪元素。

```css
@media print {
  a[href]:after {
    content: "(" attr(href) ")";
  }
}
```

## 参考链接

- [Print CSS basics in 10 minutes](https://www.paperplane.app/blog/print-css-basics/), Paperplay

