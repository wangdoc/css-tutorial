# Table 布局

CSS 可以让 HTML 元素像表格那样排列。

下面是表格的各个 HTML 标签，所对应的布局模式。

- table    { display: table }
- tr       { display: table-row }
- thead    { display: table-header-group }
- tbody    { display: table-row-group }
- tfoot    { display: table-footer-group }
- col      { display: table-column }
- colgroup { display: table-column-group }
- td, th   { display: table-cell }
- caption  { display: table-caption }

表格布局可以很简单地做到垂直居中。

```css
div {
  height: 200px;
  display:table-cell;
  vertical-align: middle;
}
```

这种写法相比下面的写法，更容易理解。

```css
div {
  height: 200px;
  position: relative;
  top: 50%;
  transform: translateY(-50%);
}
```

表格布局的另一个用途是，让页尾总是显示在浏览器的最低部，即使页面高度不足一页。

```css
/*
  HTML 代码如下
  <body>
    <div class="main"></div>
    <div class="footer"></div>
  </body>
*/

body {
  display: table;
  width: 100%;
}

.main {
  min-height: 100%;
}

.footer {
  display: table-row;
  height:1px;
}
```

基于上面这种底部固定的技巧，可以使用表格布局，完成圣杯布局，即页面从上到下分成页首 + 内容 + 页尾三部分，其中内容部分又分成左边栏和右边栏。

```css
/*
  HTML 代码如下
<div class="wrapper">
  <div class="header">HEADER</div>
  <div class="main">
    <div class="box sidebar">Left-sidebar</div>
    <div class="box content">Main Content</div>
    <div class="box sidebar">Right-sidebar</div>
  </div>
  <div class="footer">FOOTER</div>
</div>
*/

.wrapper {
  min-height: 100%;
  display: table;
  width: 100%;
  text-align: center;
}

.header {
  display: table-row;
  height: 1px;
}

.main {
  min-height: 100%;
  display: table;
  width: 100%;
}

.box {
  display: table-cell;
}

.sidebar {
  width: 100px;
}

.footer {
  display: table-row;
  height:1px;
}
```

利用表格的不同性质的行，可以调整行的显示位置。

- `display:table-caption`使得该行显示在表格的最顶部。
- `display:table-header-group`使得该行显示在表格的头部，但是位置低于`table-caption`的行。
- `display:table-footer-group`使得该行显示在表格的底部。

## 参考链接

- Colin Toh, [The Anti-hero of CSS Layout - "display:table"](https://colintoh.com/blog/display-table-anti-hero)
- Ian Devlin, [CSS stacking with display:table](https://iandevlin.com/blog/2013/06/css/css-stacking-with-display-table/)
- Ben Frain, [CSS performance test: Flexbox v CSS Table](https://benfrain.com/css-performance-test-flexbox-v-css-table-fight/)
