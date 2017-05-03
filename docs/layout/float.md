# float

## 简介

`float`属性指定某个元素定位在容器的左侧或右侧，文字和其他行内元素紧挨在它的旁边。

```css
h4  {
  float: left;
}
```

如果对行内元素指定`float`属性，就相当于将这个行内元素变成块级元素。

`float`属性可以取三个值。

- `left`：定位在容器的左侧
- `right`：定位在容器的右侧
- `none`：不采用浮动定位（默认值）

## 清理浮动

设置`float`属性以后，容器里面的行内元素（通常是文字）会紧贴浮动元素的边缘，进行布局。如果文字的长度小于浮动元素的高度，就会出现布局问题。

下面是一段 HTML 代码。

```html
<div>
  <h2>标题一</h2>
  Hello World
</div>
<h3>标题二</h3>
```

其中的“标题一”是浮动的。

```css
h2 {
  height: 200px;
  float: left;
}
```

由于`Hello World`的高度小于“标题一”的高度，导致紧跟在后面的“标题二”，不是出现在“标题一”的下方，而是在“标题一”的右侧。这时就需要清理浮动。

```css
h3 {
  clear: both;
}
```

`clear`属性可以取四个值。

- `left`：左侧不能有浮动元素
- `right`：右侧不能有浮动元素
- `both`：两侧不能有浮动元素
- `none`：默认值，不需要清理浮动

另一种情况是，容器内部的文本不希望紧贴浮动的元素，这时也可以使用`clear`属性进行清理浮动。

## 对容器的影响

如果一个容器里面所有子元素都是浮动的，就会导致这个容器变成一个空容器，高度缩为`0`。因为布局的时候，浮动的所有子元素是脱离父容器计算位置的，这导致渲染引擎认为这个容器是空元素。

解决这个问题，有三种方法。

（1）父容器也进行浮动。

```css
.container-with-float{
    float: left;
    width: 100%;
}
```

（2）父容器添加`overflow: hidden`

```css
.container-with-overflow{
    overflow: hidden;
}
```

添加`overflow: hidden`以后，容器计算高度的时候，就会自动将浮动的子元素考虑在内。

（3）CSS 生成内容

CSS 生成内容以后，就不会被渲染引擎当成是一个空元素。

```css
.container-with-generated-content:after{
    content: ".";
    display: block;
    height: 0;
    clear: both;
    visibility: hidden;
}
```

还有另一种写法。

```css
.grid:after {
  content: "";
  display: table;
  clear: both;
}
```

