# 响应式布局：media query

响应式布局（responsive）的含义是，网页会根据不同的媒介，自动采用不同的 CSS 规则。它主要通过 media 命令实现。

`media`命令用来规定 CSS 规则生效的媒介。`@media`命令后面使用关键词，指定生效的条件。

```css
@media print {
   …
}

@media screen {
   …
}
```

上面代码中，打印和显示屏分别使用不同的 CSS 规则。

媒介名称之前，还可以使用`not`和`only`关键字。

```css
@media not screen {
   …
}

@media only screen {
   …
}
```

`@media`还允许使用表达式，指定 CSS 生效的条件。表达式可以放在圆括号之中。

```css
@media (min-width: 800px) {
  p {
    font-size: 18px;
  }
}
```

上面代码中，`media`命令规定，只有在屏幕宽度大于等于`800px`时，`p`元素的大小才等于`18px`。

如果同时需要满足多个条件，可以使用`and`关键字。下面的例子是为不同的设备指定不同的背景图片。

```css
/* default is desktop image */
.someElement { background-image: url(sunset.jpg); }

@media only screen and (max-width : 1024px) {
  .someElement { background-image: url(sunset-small.jpg); }
}
```

下面是另一个例子。

```css
.component__header {
  font-size: 2rem;
  @media (min-width: 1200px) {
    font-size: 3rem
  }
}

@media only screen
  and (max-width : 603px)
  and (max-height : 966px) {
  /* Styles here */
}
```
