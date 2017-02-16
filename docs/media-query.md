# mediaQuery的用法

`media`命令的含义是，规定CSS规则生效的媒介。

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
