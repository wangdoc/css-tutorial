# 基本操作

## 垂直置中

（1）方法一

原理：子元素的 top, right, bottom, left, margin, and padding属性，针对的是父元素的维度；transform针对的子元素本身的维度。

父元素、子元素需有明确高度，不能是auto。

```css

.children{
	background: #ffdb4c;
	height: 300px;
	position: relative;
	top: 50%;
	transform: translateY(-50%);
}

```

（2）方法二

```css

.parent { position: relative; }

.child {
    position: absolute;

    left: 50%;
    top: 50%;

    -webkit-transform: translate(-50%, -50%);
    -moz-transform: translate(-50%, -50%);
    -ms-transform: translate(-50%, -50%);
    -o-transform: translate(-50%, -50%);
    transform: translate(-50%, -50%);
}

```

（3）方法三

```css
.parent { display: table; }

.child {
  display: table-cell;
  vertical-align: middle;
}
```

（5）行内置中

```css
.parent { line-height: 500px; }

.child {
    display: inline-block;
    vertical-align: middle;
}
```

（6）方法四（只对图片有效）

```css
.thumb {
  background-image: url(my-img.jpg);
  background-position: center;
  /* is this supported by IE8? I don't know */
  background-size: cover;

  height: 0;
  overflow: hidden;
  padding-bottom: 50%;
  width: 50%;
}
```

（7）方法五

```css
.children {
  margin-top: calc(50% - 12.5%);
}
```

（8）方法六

```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

（9）参考链接

- [Alignment and sizing in CSS](https://github.com/timseverien/timseverien.github.io/blob/master/_posts/2013-11-25-css-alignment-and-sizing.md)

## 清理浮动

```css

.clearfix:after{
  visibility:hidden;
  display:block;
  font-size:0;
  content:" ";
  clear:both;
  height:0;
}

.clearfix{
  zoom:1; /* for IE6 IE7 */
}

```

