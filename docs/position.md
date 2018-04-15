# position

`static`是`position`属性的默认值，表示元素在文档布局里面的正常位置。静态元素不能指定`top`、`left`等表示位置的属性。

`absolute`表示当前元素相对于它的容器元素的绝对位置。它独立于其他元素，不再是正常内容布局的一部分。绝对定位元素的容器元素，是它最近一层不是`static`布局的元素，如果没有的话，就是相对于`document`元素的布局。

`fixed`表示元素位置相对于浏览器窗口是固定的。这个元素总是可见，而且不会随着页面滚动而滚动。固定定位的元素，独立于其他元素，不是正常内容布局的一部分。

`relative`表示元素的位置是相对于它的正常位置。它依然属于内容布局的一部分，周边元素不受它的位置改变的影响。

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

