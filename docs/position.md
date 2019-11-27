# position

`position`属性用来指定一个元素在网页上的位置，一共有5种定位方式，即`position`属性主要有五个值。

> - `static`
> - `relative`
> - `fixed`
> - `absolute`
> - `sticky`

下面就依次介绍这五个值。

## static 属性值

`static`是`position`属性的默认值。如果省略`position`属性，浏览器就认为该元素是`static`定位。

这时，浏览器会按照源码的顺序，决定每个元素的位置，这称为“正常的页面流”（normal flow）。每个块级元素占据自己的区块（block），元素与元素之间不产生重叠，这个位置就是元素的默认位置。

![](https://www.wangbase.com/blogimg/asset/201911/bg2019111720.jpg)

注意，`static`定位所导致的元素位置，是浏览器自主决定的，所以这时`top`、`bottom`、`left`、`right`这四个属性无效。

## relative，absolute，fixed

`relative`、`absolute`、`fixed`这三个属性值有一个共同点，都是相对于某个基点的定位，不同之处仅仅在于基点不同。所以，只要理解了它们的基点是什么，就很容易掌握这三个属性值。

这三种定位都不会对其他元素的位置产生影响，即不管有没有这个元素，其他元素的位置不变，因此元素之间可能产生重叠。

### relative 属性值

`relative`表示，相对于默认位置（即`static`时的位置）进行偏移，即定位基点是元素的默认位置。

![](https://www.wangbase.com/blogimg/asset/201911/bg2019111721.jpg)

![](https://www.wangbase.com/blogimg/asset/201911/bg2019111722.jpg)

它必须搭配`top`、`bottom`、`left`、`right`这四个属性一起使用，用来指定偏移的方向和距离。

![](https://www.wangbase.com/blogimg/asset/201911/bg2019111723.jpg)

```css
div {
  position: relative;
  top: 20px;
}
```

上面代码中，`div`元素从默认位置向下偏移`20px`（即距离顶部`20px`）。

### absolute 属性值

`absolute`表示，相对于祖先元素（一般是父元素）进行偏移，即定位基点通常是父元素。

它有一个重要的限制条件：父元素不能是`static`定位，否则定位基点会移到最近一个非`static`定位的祖先元素。如果所有祖先元素都是`static`定位，定位基点就变成整个网页的根元素`html`。另外，`absolute`定位也必须搭配`top`、`bottom`、`left`、`right`这四个属性一起使用。

![](https://www.wangbase.com/blogimg/asset/201911/bg2019111801.jpg)

```css
/*
  HTML 代码如下
  <div id="father">
    <div id="son"></div>
  </div>
*/

#father {
  positon: relative;
}
#son {
  position: absolute;
  top: 20px;
}
```

上面代码中，父元素是`relative`定位，子元素是`absolute`定位，所以子元素的定位基点是父元素，相对于父元素的顶部向下偏移`20px`。如果父元素是`static`定位，上例的子元素就是距离网页的顶部向下偏移`20px`。

注意，`absolute`定位的元素会被“正常页面流”忽略，即在“正常页面流”中，该元素所占空间为零，周边元素不受影响。

### fixed 属性值

`fixed`表示，相对于视口（viewport，浏览器窗口）进行偏移，即定位基点是浏览器窗口。这会导致元素的位置不随页面滚动而变化，好像固定在网页上一样。

![](https://www.wangbase.com/blogimg/asset/201911/bg2019111802.jpg)

它如果搭配`top`、`bottom`、`left`、`right`这四个属性一起使用，表示元素的初始位置是基于视口计算的，否则初始位置就是元素的默认位置。

```css
div {
  position: fixed;
  top: 0;
}
```

上面代码中，`div`元素始终在视口顶部，不随网页滚动而变化。

## 四、sticky 属性值

`sticky`跟前面四个属性值都不一样，它会产生动态效果，很像`relative`和`fixed`的结合：一些时候是`relative`定位（定位基点是自身默认位置），另一些时候自动变成`fixed`定位（定位基点是视口）。

因此，它能够形成“动态固定”的效果。比如，网页的搜索工具栏，初始加载时在自己的默认位置（`relative`定位）。

![](https://www.wangbase.com/blogimg/asset/201911/bg2019111604.jpg)

页面向下滚动时，工具栏变成固定位置，始终停留在页面头部（`fixed`定位）。

![](https://www.wangbase.com/blogimg/asset/201911/bg2019111605.jpg)

等到页面重新向上滚动回到原位，工具栏也会回到默认位置。

`sticky`生效的前提是，必须搭配`top`、`bottom`、`left`、`right`这四个属性一起使用，不能省略，否则等同于`relative`定位，不产生“动态固定”的效果。原因是这四个属性用来定义“偏移距离”，浏览器把它当作`sticky`的生效门槛。

它的具体规则是，当页面滚动，父元素开始脱离视口时（即部分不可见），只要与`sticky`元素的距离达到生效门槛，`relative`定位自动切换为`fixed`定位；等到父元素完全脱离视口时（即完全不可见），`fixed`定位自动切换回`relative`定位。

请看下面的示例代码。（注意，除了已被淘汰的 IE 以外，其他浏览器目前都支持`sticky`。但是，Safari 浏览器需要加上浏览器前缀`-webkit-`。）

```css
#toolbar {
  position: -webkit-sticky; /* safari 浏览器 */
  position: sticky; /* 其他浏览器 */
  top: 20px;
}
```

上面代码中，页面向下滚动时，`#toolbar`的父元素开始脱离视口，一旦视口的顶部与`#toolbar`的距离小于`20px`（门槛值），`#toolbar`就自动变为`fixed`定位，保持与视口顶部`20px`的距离。页面继续向下滚动，父元素彻底离开视口（即整个父元素完全不可见），`#toolbar`恢复成`relative`定位。

## 五、 sticky 的应用

`sticky`定位可以实现一些很有用的效果。除了上面提到“动态固定”效果，这里再介绍两个。

## 5.1 堆叠效果

堆叠效果（stacking）指的是页面滚动时，下方的元素覆盖上方的元素。下面是一个图片堆叠的例子，下方的图片会随着页面滚动，覆盖上方的图片（查看 [demo](https://jsbin.com/fegiqoquki/edit?html,css,output)）。

![](https://www.wangbase.com/blogimg/asset/201911/bg2019111609.jpg)

HTML 代码就是几张图片。

```html
<div><img src="pic1.jpg"></div>
<div><img src="pic2.jpg"></div>
<div><img src="pic3.jpg"></div>
```

CSS 代码极其简单，只要两行。

```css
div {
  position: sticky;
  top: 0;
}
```

它的原理是页面向下滚动时，每张图片都会变成`fixed`定位，导致后一张图片重叠在前一张图片上面。详细解释可以看[这里](https://dev.to/vinceumo/slide-stacking-effect-using-position-sticky-91f)。

### 5.2 表格的表头锁定

大型表格滚动的时候，表头始终固定，也可以用`sticky`实现（查看 [demo](https://jsbin.com/decemanohe/edit?html,css,output)）。

![](https://www.wangbase.com/blogimg/asset/201911/bg2019111610.jpg)

CSS 代码也很简单。

```css
th {
  position: sticky;
  top: 0; 
}
```

需要注意的是，`sticky`必须设在`<th>`元素上面，不能设在`<thead>`和`<tr>`元素，因为这两个元素没有`relative`定位，也就无法产生`sticky`效果。详细解释可以看[这里](https://css-tricks.com/position-sticky-and-table-headers/)。

## z-index

`z-index`表示元素重叠时的层次关系。这个值越高，对应的元素就在越上层。所有元素的默认`z-index`是0。

由于静态布局的元素不会产生重叠，所以该属性对静态元素无效。只有元素是非静态布局（即`position`属性的值不是`static`），`z-index`属性才有意义。如果没有设置`z-index`，元素重叠时，HTML 代码中越后面出现的元素在越上层。

`z-index`属性的难点在于，一组设置了`z-index`属性的元素，它们的堆叠顺序取决于，它们是否处在同一个堆叠上下文（stacking context）。三种情况会创建堆叠上下文。

- 网页的根元素（即`<html>`元素）
- 网页元素是非静态布局，且`z-index`属性不等于`auto`
- 网页元素的`opacity`属性小于1

同一个堆叠上下文之中，元素的堆叠（从下层到上层）按照以下顺序决定。

- 堆叠上下文的根元素
- 设置了定位、且`z-index`为负值的元素
- 没有设置定位的元素
- 设置了定位、且`z-index`为`auto`的元素
- 设置了定位、且`z-index`为正值的元素

```css
/* HTML 代码如下
<div id="container">
  <div id="item-a">A</div>
  <div id="item-b">b</div>
</div>
<div id="item-c">C</div>
*/

div {
  width: 100px;
  height: 100px;
}

#item-a {
  background-color: red;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 3;
}

#item-b {
  background-color: blue;
  position: absolute;
  top: 20px;
  left: 20px;
  z-index: 2;
}

#item-c {
  background-color: yellow;
  position: absolute;
  top: 40px;
  left: 40px;
  z-index: 1;
}
```

上面代码中，`item-a`在最上层，然后是`item-b`，最下层是`item-c`。

现在，对`item-a`和`item-b`父元素`container`设一下定位。

```css
#container {
  position: relative;
  z-index: 0;
}
/* 或者写成
#container {
  opacity: 0.99;
}
*/
```

结果就会变成`item-c`在最上层，然后是`item-a`，最下层是`item-b`。这是因为这时`container`形成一个独立的堆叠上下文，`item-a`和`item-b`处在这个上下文之中，与`item-c`不再是同一个层级的关系了。

## 参考链接

- [What No One Told You About Z-Index](https://philipwalton.com/articles/what-no-one-told-you-about-z-index/), by Philip Walton

