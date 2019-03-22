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

**（1）repeat()**

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

**（2）auto-fill 关键字**

还有一种情况，单元格的大小是固定的，但是容器的大小不确定，比如容器是全屏，但不知道用户的屏幕有多大。这时，我们希望每一行（或每一列），容纳尽可能多的单元格，这时可以使用`auto-fill`关键字表示自动填充。

```css
.container {
  display: grid;
  grid-template-columns: repeat(auto-fill, 100px);
}
```

[上面代码](https://jsbin.com/himoku/edit?css,output)表示每列宽度`100px`，然后自动填充，直到容器不能放置更多的列。

**（3）fr 关键字**

为了方便表示比例关系，网格布局提供了`fr`关键字（fraction 的缩写，意为“片段”）。

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr;
}
```

[上面代码](https://jsbin.com/hadexek/edit?html,css,output)表示三个相同宽度的列，三个相同高度的行。

`fr`可以与绝对长度的单位结合使用，这时会非常方便。

```css
.container {
  display: grid;
  grid-template-columns: 150px 1fr 2fr;
}
```

上面代码表示，第一列的宽度为150像素，第二列的宽度则是第三列的一半。

**（4）max-content 关键字，min-content 关键字**

`max-content`关键字表示宽度（高度）与本栏（本列）内容宽度最大（高度最大）的单元格相同。

`min-content`关键字表示宽度（高度）等于本栏（本列）内容宽度最小（高度最小）的单元格相同。

```css
.container {
  display: grid;
  grid-template-columns: 150px max-content min-content;
}
```

上面代码表示，第一列的宽度为150像素，第二列的宽度等于该列最宽的单元格，第三列的宽度等于该列最窄的单元格。

**（5）minmax()**

`minmax()`函数列出一个长度范围。它接受两个参数，第一个参数表示下限值，第二个参数表示上限值。如果当前列（行）的宽度（高度）小于下限值，则使用下限值；如果大于上限值，则使用上限值；否则，就使用实际值。

```css
grid-template-columns: 1fr 1fr minmax(160px, 1fr);
grid-template-columns: 1fr 1fr minmax(160px, max-content);
```

上面代码中，`minmax(160px, 1fr)`表示列宽不小于`160px`，不大于`1fr`; `minmax(160px, max-content)`则表示列宽最大不超过实际宽度。

**（6）auto 关键字**

`auto`关键字基本上等同于`max-content`，除非单元格内容设置了`min-width`（`min-height`），且这个下限值比`max-content`还要大，这时就会等于`min-width`（`min-height`）。

```css
grid-template-columns: 100px auto 100px;
```

上面代码中，第二列的宽度，基本上等于该列单元格的最大宽度，除非单元格内容设置了`min-width`，且这个下限值大于最大宽度，这时第二列的宽度就会等于下限值。

**（7）网格线的名称**

`grid-template-columns`属性和`grid-template-rows`属性里面，还可以使用方括号，指定每一根网格线的名字，方便以后的引用。

```css
.container {
  display: grid;
  grid-template-columns: [c1] 100px [c2] 100px [c3] auto [c4];
  grid-template-rows: [r1] 100px [r2] 100px [r3] auto [r4];
}
```

上面代码指定网格布局为3行乘3列，因此有4根垂直网格线和4根水平网格线。方括号里面依次是这八根线的名字。

网格布局允许，同一根线有多个名字，比如`[fifth-line row-5]`。

### grid-row-gap 属性，grid-column-gap 属性，grid-gap 属性

`grid-row-gap`属性设置行与行的间隔（行间距），`grid-column-gap`属性设置列与列的间隔（列间距）。

```css
.container {
  grid-row-gap: 20px;
  grid-column-gap: 20px;
}
```

[上面代码](https://jsbin.com/mezufab/edit?css,output)中，`grid-row-gap`用于设置行间距，`grid-column-gap`用于设置列间距。

`grid-gap`属性是`grid-column-gap`和`grid-row-gap`的简写形式，使用方式如下。

```css
grid-gap: <grid-row-gap> <grid-column-gap>;
```

因此，上面一段 CSS 代码等同于下面的代码。

```css
.container {
  grid-gap: 20px 20px;
}
```

如果`grid-row-gap`和`grid-column-gap`的值相等，`grid-gap`可以只写一个值。

```css
.container {
  grid-gap: 20px;
}
```

注意，根据最新标准，这些属性里面的`grid-`前缀已经删除，`grid-column-gap`和`grid-row-gap`写成`column-gap`和`row-gap`，`grid-gap`写成`gap`。

### grid-template-areas 属性

网格布局允许多个单元格组成一个“区域”（area），单个单元格的区域也是允许的。`grid-template-areas`属性用于定义区域。

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

上面代码先划分出9个单元格，然后将定名为`a`到`i`的九个区域，分别对应这九个单元格。

一个区域包括多个单元格的写法如下。

```css
grid-template-areas: 'a a a'
                     'b b b'
                     'c c c';
```

上面代码将9个单元格分成`a`、`b`、`c`三个区域。

区域可以用来为布局的各个部分，指定有意义的名称。

```css
grid-template-areas: "header header header"
                     "main main sidebar"
                     "footer footer footer";
```

上面代码中，网页顶部是页眉`header`，底部是页脚`footer`，中间部分则为`main`和`sidebar`。

如果有的区域为空，不需要利用，则使用“点”（`.`）表示。

```css
grid-template-areas: 'a . c'
                     'd . f'
                     'g . i';
```

上面代码中，中间一列为点，表示没有用到该单元格，或者该单元格不属于任何区域。

注意，区域的命名会影响到网格线。每个区域的起始网格线，会自动命名为区域名加上`-start`后缀，终止网格线自动命名为区域名加上`-end`后缀。比如，区域名为`header`，则该区域起始位置的水平网格线和垂直网格线叫做`header-start`，终止位置的水平网格线和垂直网格线叫做`header-end`。

### grid-auto-flow 属性

划分网格以后，容器的子元素会按照顺序，自动放置在每一个网格。默认的放置顺序是“先行后列”，即先填满第一行，然后再开始放入第二行，即下图数字的顺序。

放置顺序由`grid-auto-flow`属性决定，默认值是`row`，即“先行后列”。也可以将它设成`column`，变成“先列后行”。

```css
grid-auto-flow: column;
```

上面代码设置了`column`以后，放置顺序就变成了下图。

`grid-auto-flow`属性除了设置成`row`和`column`，还可以设成`row dense`和`column dense`。这两个值主要用于，某些位置被指定项目占据了以后，剩下的单元格怎么自动放置。

如果指定`1`号项目占据第一行第一列，`9`号项目占据第三行第一列，剩下的项目自动排列。

```css
grid-auto-flow: row dense;
```

[上面代码](https://jsbin.com/wapejok/edit?css,output)表示，优先填满行，效果如下图。`dense`关键字表示紧密填充，尽量不出现空格。

```css
grid-auto-flow: column dense;
```

[上面代码](https://jsbin.com/moyeduf/edit?css,output)表示，优先填满列，效果如下图。

### justify-items 属性，align-items 属性，place-items 属性

`justify-items`属性设置单元格内容的水平位置（左中右），`align-items`属性设置单元格内容的垂直位置（上中下）。

```css
.container {
  justify-items: start | end | center | stretch;
  align-items: start | end | center | stretch;
}
```

这两个属性的写法完全相同，都可以取下面这些值。

- start：对齐单元格的起始边缘。
- end：对齐单元格的结束边缘。
- center：单元格内部居中。
- stretch：拉伸，占满单元格的整个宽度（默认值）。

```css
.container {
  justify-items: start;
}
```

[上面代码](https://jsbin.com/gijeqej/edit?css,output)表示，单元格的内容左对齐。

```css
.container {
  align-items: start;
}
```

[上面代码](https://jsbin.com/tecawur/edit?css,output)表示，单元格的内容头部对齐。

`place-items`属性则是`align-items`属性和`justify-items`属性的简写形式。

```css
place-items: <align-items> <justify-items>;
```

下面是一个例子。

```css
place-items: start end;
```

如果省略第二个值，则浏览器认为与第一个值相等。

```css
place-items: center;
/* 等同于 */
place-items: center center;
```

### justify-content 属性，align-content 属性，place-content 属性

`justify-content`属性是整个内容区域在容器里面的水平位置（左中右），`align-content`属性是整个内容区域的垂直位置（上中下）。

```css
.container {
  justify-content: start | end | center | stretch | space-around | space-between | space-evenly;
  align-content: start | end | center | stretch | space-around | space-between | space-evenly;  
}
```

这两个属性的写法完全相同，都可以取下面这些值。

- start - 对齐容器的起始边框。
- end - 对齐容器的结束边框。
- center - 容器内部居中。
- stretch - 项目大小没有指定时，拉伸占据整个网格容器。
- space-around - 每个项目两侧的间隔相等。所以，项目之间的间隔比项目与容器边框的间隔大一倍。
- space-between - 项目与项目的间隔相等，项目与容器边框之间没有间隔。
- space-evenly - 项目与项目的间隔相等，项目与容器边框之间也是同样长度的间隔。

```css
align-content: end;
```

上面代码的效果如下图。

`place-content`属性是`align-content`属性和`justify-content`属性的简写形式。

```css
place-content: <align-content> <justify-content>
```

下面是一个例子。

```css
place-content: space-around space-evenly;
```

如果省略第二个值，浏览器就会假定第二个值等于第一个值。

### grid-auto-columns 属性，grid-auto-rows 属性

有时候，一些项目的指定位置，在现有网格的外部。比如网格只有3列，但是某一个项目指定在第5行。这时，浏览器会自动生成多余的网格，以便放置项目。

`grid-auto-columns`属性和`grid-auto-rows`属性用来设置，浏览器自动创建的多余网格的列宽和行高。它们的写法与`grid-template-columns`和`grid-template-rows`完全相同。如果不指定这两个属性，浏览器完全根据单元格内容的大小，决定新增网格的列宽和行高。

[下面的例子](https://jsbin.com/sayuric/edit?css,output)里面，划分好的网格是3行 x 3列，但是，8号项目指定在第4行，9号项目指定在第5行。

```css
.container {
  grid-auto-rows: 50px;
}
```

上面代码指定新增的行高统一为50px（原始的行高为100px）。

### grid-template 属性，grid 属性

`grid-template`属性是`grid-template-columns`、`grid-template-rows`和`grid-template-areas`这三个属性的合并简写形式。

`grid`属性是`grid-template-rows`、`grid-template-columns`、`grid-template-areas`、  `grid-auto-rows`、`grid-auto-columns`、`grid-auto-flow`这六个属性的合并简写形式。

从易读易写的角度考虑，还是建议不要合并属性，所以这里就不详细介绍这两个属性了。

## 项目属性

下面这些属性定义在项目上面。

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

