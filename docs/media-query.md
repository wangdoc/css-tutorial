# 响应式布局：media query

响应式布局（responsive）的含义是，网页会根据不同的媒介，自动采用不同的 CSS 规则。它主要通过 media 命令实现。

`media`命令的含义是，规定CSS规则生效的媒介。

```css
@media (min-width: 800px) {
  p {
    font-size: 18px;
  }
}
```

上面代码中，`media`命令规定，只有在屏幕宽度大于等于`800px`时，`p`元素的大小才等于`18px`。

`media`命令的一种用法是，为不同的设备指定不同的背景图片。

```css
/* default is desktop image */
.someElement { background-image: url(sunset.jpg); }

@media only screen and (max-width : 1024px) {
  .someElement { background-image: url(sunset-small.jpg); }
}
```


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
