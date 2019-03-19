# CSS Grid

## 概述

网格布局（Grid）是最强大的 CSS 布局方案。

它将网页空间划分成一个个网格，然后像乐高积木那样，允许你任意组合不同的网格，做出各种各样的布局。以前，你只能通过复杂的 CSS 框架库达到的效果，现在浏览器内置提供了。

上图这样的布局，就是 Grid 布局的效果。

除了 Grid 布局，CSS 还支持 Flex 布局。这两种布局有一定的相似性，都可以指定容器内部多个项目的位置。但是，它们也存在重大区别。

Flex 布局是轴线布局（主轴和交叉轴），只能指定项目针对轴线的位置，可以看作是一维布局。Grid 布局是将容器划分成“行”和“列”（即划分单元格），然后指定项目所在的单元格，可以看作是二维布局。Grid 布局远比 Flex 布局强大。

## 基本概念

学习 Grid 布局之前，需要了解一些专门术语。

**（1）容器**

采用网格布局的那个区域，称为“容器”（container）。

**（2）项目**

在容器内部，采用网格定位的子元素，称为“项目”（item）。

```html
<div>
  <div><p>1</p></div>
  <div><p>2</p></div>
  <div><p>3</p></div>
</div>
```

上面代码中，外层的`<div>`元素就是容器，内层的三个`<div>`元素就是项目。

注意：项目只能是容器的顶层子元素，不包含项目的子元素，比如上面代码的`<p>`元素。Grid 布局只对项目有效。

**（3）行**

容器里面水平的区域，称为“行”（row）。

**（4）列**

容器里面垂直的区域，称为“列”（column）。

上图中，水平的深色区域就是“行”，垂直的深色区域就是（列）。

**（5）单元格**

行和列的交叉区域，称为“单元格”（cell）。

正常情况下，`n`行和`m`列会产生`n x m`个单元格。比如，3行3列会产生9个单元格。

**（6）网格线**

划分网格的线，称为“网格线”（grid line）。划分“行”的网格线，称为水平网格线；划分“列”的网格线，称为垂直网格线。

正常情况下，`n`行有`n + 1`根水平网格线，`m`列有`m + 1`根垂直网格线，比如三行有四根网格线。

上图是一个 4 x 4 的网格，共有5根水平网格线和5根垂直网格线。

## 容器属性

网格布局的属性分成两部分，一部分属于容器属性，另一部分属于项目属性。这里先介绍容器属性。

### display 属性

`display: grid`可以指定一个容器为网格布局。

```css
div {
  display: grid;
}
```

默认情况下，容器元素都是块级元素，但也可以设成行内元素。

```css
div {
  display: inline-grid;
}
```

上面代码指定`div`是一个行内元素，然后该元素内部是网格布局。

上图是网格容器嵌在一段文本之中。第一张图是`display: grid`的[效果](https://jsbin.com/guvivum/edit?html,css,output)，第二张图是`display: inline-grid`的[效果](https://jsbin.com/purojey/edit?html,css,output)。

注意，设为网格布局以后，容器的`float`、`display: inline-block`、`display: table-cell`、`vertical-align`和`column-*`这些设置都将失效。

### grid-template-columns 属性，grid-template-rows 属性

设置了`display: grid`以后，下一步就是要指定容器分成多少行和多少列。

`grid-template-columns`属性用来定义每一列的列宽，`grid-template-rows`属性则是定义每一行的行宽。

```css
.container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px 100px;
}
```

[上面代码](https://jsbin.com/qiginur/edit?css,output)指定了一个三行三列的网格，列宽和行高都是`100px`。

除了使用绝对单位，这里也允许使用百分比。

```css
.container {
  display: grid;
  grid-template-columns: 33.33% 33.33% 33.33%;
  grid-template-rows: 33.33% 33.33% 33.33%;
}
```

有时候，重复写同样的值非常麻烦，尤其网格很多时。这时，可以使用`repeat()`函数，简化重复的值。

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 33.33%);
  grid-template-rows: repeat(3, 33.33%);
}
```

`repeat()`重复某种模式也是可以的。

```css
grid-template-columns: repeat(2, 100px 20px 80px);
```

[上面代码](https://jsbin.com/cokohu/edit?css,output)定义了6列，第一列和第四列的宽度为`100px`，第二列和第五列为`20px`，第三列和第六列为`80px`。

还有一种情况，单元格的大小是固定的，但是容器的大小不确定，比如容器是全屏，但不知道用户的屏幕有多大。这时，我们希望每一行（或每一列），容纳尽可能多的单元格，这时可以使用`auto-fill`关键字表示自动填充。

```css
.container {
  display: grid;
  grid-template-columns: repeat(auto-fill, 100px);
}
```

[上面代码](https://jsbin.com/himoku/edit?css,output)表示每列宽度`100px`，然后自动填充，直到容器不能放置更多的列。

### fr 关键字

有时候，计算百分比不是很方便，这时可以使用`fr`关键字（fraction 的缩写），下面的代码可以取得一样的效果。

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr;
}
```

`fr`可以与绝对单位结合使用，这时会非常方便。

```css
.container {
  display: grid;
  grid-template-columns: 150px 1fr 2fr;
}
```

`grid-template-columns`属性和`grid-template-rows`属性都允许使用`auto`关键字，表示占据剩余的所有宽度。

```css
.container {
  display: grid;
  grid-template-columns: 100px auto 100px;
  grid-template-rows: 100px auto 100px;
}
```

有时候，希望为网格指定最小值或最大值，这时可以使用`minmax()`函数设置一个数值范围。

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr minmax(160px, 1fr);
}
```

上面代码中，`minmax(160px, 1fr)`表示该列的列宽不小于`160px`，不大于`1fr`。

### 网格线的名字

`grid-template-columns`属性和`grid-template-rows`属性里面，还可以指定网格线的名字。

```css
.container {
  display: grid;
  grid-template-columns: [c1] 100px [c2] 100px [c3] auto [c4];
  grid-template-rows: [r1] 100px [r2] 100px [r3] auto [r4];
}
```

上面代码指定网格布局为三行乘三列，因此有四根竖线和四根横线。方括号里面依次是这八根线的名字。

可以为同一根线，指定多个名字`[main-end footer-start row-5]`。

每个区域的起始线和终止线，会有自动的名字。比如，区域名为`header`，则区域的起始行线和起始列线叫做`header-start`，终止行线和终止列线叫做`header-end`。

这两个属性之中，允许为每根网格线指定名称。

```css
.container{
  grid-template-columns: [first] 40px [line2] 50px [line3] auto [col4-start] 50px [five] 40px [end];
  grid-template-rows: [row1-start] 25% [row1-end] 100% [third-line] auto [last-line];
}
```

注意，网格线的名称可以相同，而且每根网格线可以有不止一个的名称。

```css
.container{
  grid-template-rows: [row1-start] 25% [row1-end row2-start] 25% [row2-end];
}
```

### grid-template 属性

`grid-template`属性是`grid-template-columns`、`grid-template-rows`和`grid-template-areas`属性的简写形式。这里不详细介绍了。

### grid-row-gap 属性，grid-column-gap 属性，grid-gap 属性

`grid-row-gap`属性设置行与行的间隔（行间距），`grid-column-gap`属性设置列与列的间隔（列间距）。

```css
.container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px 100px;
  grid-row-gap: 20px;
  grid-column-gap: 20px;
}
```

上面代码中，`grid-row-gap`用于设置行间距，`grid-column-gap`用于设置列间距。如果两个值都相等，可以写成`grid-gap`。

`grid-gap`属性是`grid-column-gap`和`grid-row-gap`的简写形式。

```css
.container {
  display: grid;
  grid-gap: <grid-row-gap> <grid-column-gap>;
}
```

如果`grid-row-gap`和`grid-column-gap`的值相等，`grid-gap`可以只写一个值。

```css
.container {
  display: grid;
  grid-gap: 20px;
}
```

注意，`grid-`前缀将被删除，`grid-column-gap`和`grid-row-gap`也可以写为`column-gap`和`row-gap`，`grid-gap`也可以写为`gap`。

### grid-template-areas 属性

`grid-template-areas`属性用于为单元格起名。

```css
.container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px 100px;
  grid-template-areas: 'a b c'
                       'd e f'
                       'g h i';
}
```

上面代码将9个单元格分别命名为`a`到`i`。

`grid-template-areas`属性允许多个单元格重名，相当于将多个单元格合并组成了一个区域。

```css
.container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px 100px;
  grid-template-areas: 'a a a'
                       'b b b'
                       'c c c';
}
```

上面代码将9个单元格分成`a`、`b`、`c`三个区域。

这可以用来为网页划分区域。

```css
grid-template-areas: "header header header"
                     "main main sidebar"
                     "footer footer footer";
```

上面代码划分出页眉`header`和页脚`footer`，中间部分则为`main`和`sidebar`。

如果有的区域为空，不需要利用，则使用“点”（`.`）表示。

```css
grid-template-areas: 'a . c'
                     'd . f'
                     'g . i';
```

上面代码中，中间一列为点，表示没有用到。

### grid-auto-flow 属性

容器元素的子元素会依次自动放入网格，这由`grid-auto-flow`属性决定。它的默认值是`row`，即网格编号的默认顺序，是先从左到右，再从上到下，即先行后列。也可以将它设成`column`，从先列后行。

```css
grid-auto-flow: column;
```

`row dense`和`column dense`表示，某几个单元格指定内容以后，剩余的单元格应该先填满行，还是先填满列。

`dense`关键字表示紧密填充，尽量不出现空格。

```css
grid-auto-flow: row dense;
```

### justify-items 属性，align-items 属性，place-items 属性

`justify-items`属性设置单元格内部如何水平对齐。

```css
.container {
  justify-items: start | end | center | stretch;
}
```

它可以取以下的值。

- start - 与单元格的起始边缘齐平
- end - 与单元格的结束边缘齐平
- center - 对齐单元格的中心
- stretch - 填充单元格的整个宽度（默认值）

`align-items`属性设置单元格内部如何垂直对齐。

```css
.container {
  align-items: start | end | center | stretch;
}
```

它可以取以下的值。

- start - 与单元格的起始边缘对齐
- end - 与单元格的结束边缘对齐
- center - 对齐单元格中心
- stretch - 填充单元格的整个高度（默认值）

`place-items`属性是`align-items`属性和`justify-items`属性的简写。

```css
place-items: <align-items> / <justify-items>;
```

### justify-content 属性，align-content 属性，place-content 属性

`justify-content`属性是内容区域在容器里面的水平位置。

```css
.container {
  justify-content: start | end | center | stretch | space-around | space-between | space-evenly;
}
```

它可以取以下的值。

- start - 将网格与网格容器的起始边缘对齐
- end - 将网格与网格容器的末端边缘对齐
- center - 将网格对齐网格容器的中心
- stretch - 调整网格项的大小以允许网格填充网格容器的整个宽度。
- space - 在每个网格项之间放置一个全长度的空白，在边缘放置半大小的空白。
- space-between - 每个网格项之间的间隔相等，在边缘处没有空白。
- space-evenly - 在每个网格项之间放置一个均匀的空间，包括远端

`align-content`属性是内容区域在容器里面的垂直位置。

- start - 将网格与网格容器的起始边缘齐平
- end - 将网格与网格容器的末端边缘齐平
- center - 将网格对齐网格容器的中心
- stretch - 调整网格项的大小以允许网格填充网格容器的整个高度
- space - 在每个网格项之间放置一个均匀的空间，在远端放置半个大小的空格
- space-between - 在每个网格项之间放置一个均匀的空间，在远端没有空格
- space-evenly - 在每个网格项之间放置一个均匀的空间，包括远端

`place-content`属性是`align-content`属性和`justify-content`属性的简写。

```css
place-content: <align-content> / <justify-content>
```

### grid-auto-columns 属性，grid-auto-rows 属性

`grid-auto-columns`属性和`grid-auto-rows`属性用来设置隐藏的列宽和行高。

```css
.container {
  grid-auto-columns: 60px;
}
```

这两个属性可以取以下值。

- 长度单位：比如`30px`、`20%`、`0.5fr`。
- max-content：高度或宽度最大的项目
- min-content：高度或宽度最小的项目
- minmax(min, max)：高度或宽度的范围
- auto：如果设置了`min-width`或`min-height`，则使用它们的值。否则等同于`max-content`。

这个属性可以一次性设置多行或多列。

```css
grid-auto-rows: min-content max-content auto;
grid-auto-rows: 100px 150px 390px;
grid-auto-rows: 10% 33.3%;
grid-auto-rows: 0.5fr 3fr 1fr;
```

## 项目属性

### grid-column-start 属性，grid-column-end 属性，grid-row-start 属性，grid-row-end 属性

一个项目有四根边框线，都可以指定所在的网格线的位置或名字。

- `grid-column-start`：上边框
- `grid-column-end`：下边框
- `grid-row-start`：左边框
- `grid-row-end`：右边框

```css
.item-1 {
  grid-column-start: 2;
  grid-column-end: five;
  grid-row-start: row1-start
  grid-row-end: 3;
}
```

`span`关键字表示“跨越”，它后面跟的数字表示跨越的网格数量，即两根网格线之间相隔的网格数。

```css
.item-b {
  grid-column-start: 1;
  grid-column-end: span col4-start;
  grid-row-start: 2
  grid-row-end: span 2
}
```

如果未声明`grid-column-end`或`grid-row-end`，默认将占据一个网格。

如果`grid-column-start`和`grid-row-start`使用`span`关键字，则表示从默认位置跨越1个栏位。

```css
.item-b {
  grid-column-start: span 2;
}

.container header,
.container nav,
.container footer {
  grid-column: span 4;
}
```

项目可以相互重叠，这时可以使用`z-index`控制堆叠顺序。

### grid-column 属性，grid-row 属性

`grid-column`属性是`grid-column-start`和`grid-column-end`的简写形式，`grid-row`属性是`grid-row-start`属性和`grid-row-end`的简写形式。

```css
.item {
  grid-column: <start-line> / <end-line>;
  grid-row: <start-line> / <end-line>;
}
```

下面是一个例子。

```css
.item-1 {
  background: #b03532;
  grid-column: 1 / 3;
  grid-row: 1 / 2;
}
```

上面代码中，项目`item-1`占据第一行，从第一根列线到第三根列线。

这两个属性之中，也可以使用`span`关键字，表示跨越多少个网格。

```css
.item-1 {
  background: #b03532;
  grid-column: 1 / 3;
  grid-row: 1 / 3;
}
/* 等同于 */
.item-1 {
  background: #b03532;
  grid-column: 1 / span 2;
  grid-row: 1 / span 2;
}
```

上面代码中，项目`item-1`占据的区域，包括第一行到第二行、第一列到第二列。

斜杠以及后面的部分可以省略，默认跨越一个网格。

```css
.item-1 {
  background: #b03532;
  grid-column: 1;
  grid-row: 1;
}
```

上面代码中，项目`item-1`占据第一行第一列。

### `grid-area`属性

`grid-area`属性指定项目放在哪一个区域。

```css
.item-1 {
  background: #b03532;
  grid-area: header;
}
```

此属性可用作`grid-row-start` + `grid-column-start`、`grid-row-end`、`grid-column-end`的更短缩写，直接指定项目的位置。

```css
.item {
  grid-area: <name> | <row-start> / <column-start> / <row-end> / <column-end>;
}
```

下面是一个例子。

```css
.item-d {
  grid-area: 1 / col4-start / last-line / 6;
}
```

### justify-self

`justify-self`指定项目在单元格内部的位置，可以取四个值。

- start - 项目与单元格的起始边缘对齐
- end - 项目与单元格的结束边缘对齐
- center - 项目在单元格的中心
- stretch - 项目填充单元格的整个宽度（默认值）

```css
.item {
  justify-self: start | end | center | stretch;
}
```

下面是一个例子。

```css
.item-a {
  justify-self: start;
}
```

### align-self

`align-self`属性指定项目在单元格里面的水平对齐方式。

- start - 将网格项对齐以与单元格的起始边缘齐平
- end - 将网格项对齐以与单元格的结束边缘齐平
- center - 将网格项对齐在单元格的中心
- stretch - 填充单元格的整个高度（这是默认值）

```css
.item {
  align-self: start | end | center | stretch;
}
```

下面是一个例子。

```css
.item-a {
  align-self: start;
}
```

### place-self 属性

`place-self`属性是`align-self`属性和`justify-self`属性的简写形式。

```css
place-self: <align-self> / <justify-self>;
```

如果只有一个值，则`align-self`属性和`justify-self`属性都使用这个值。

## 响应式实例

https://webdesign.tutsplus.com/tutorials/how-to-build-an-off-canvas-navigation-with-css-grid--cms-28191

## 参考链接

- https://webdesign.tutsplus.com/articles/new-course-3-css-grid-projects-for-web-designers--cms-27947
- [A Complete Guide to Grid](https://css-tricks.com/snippets/css/complete-guide-grid/), by Chris House
- [Understanding the CSS Grid Layout Module](https://webdesign.tutsplus.com/series/understanding-the-css-grid-layout-module--cms-1079), by Ian Yates

## 两栏式布局

对于两栏式布局，Grid 的写法如下。

```css
.wrapper {
  display: grid;
  grid-template-columns: 70% 30%;
  grid-gap: 2rem;
}
```

