# 字体

## font-size

`font-size`属性用于设置网页的字体大小。

下面是设置网页根字体大小的例子。

```css
:root {
  font-size: 16px;
}

/* 也可以针对 html 元素设置
html {
  font-size: 16px;
}
```

然后，每个一级区块的`font-size`采用`rem`单位，内部属性使用`em`单位。这时，`em`的大小是基于`rem`设置的。

```css
button {
    font-size: 0.875rem;
    // All the internal/external value use in 'em'
    // This value use of your "font-size" as the basic font size
    // And you will not have any problem with the font size of the container ( Example bottom )
    padding: .5em 1em;
    border: .125em solid #e3e3e3;
    @media (min-width: 48rem){ // min-width: 768px
      font-size: 1.125rem;
    }
    @media (min-width: 62rem){ // min-width: 992px
      font-size: 1.375rem;
    }
}
```

## font-smoothing

`font-smooth`属性主要用于控制浏览器对字体的渲染。比如，下面的设置可以减少字体渲染出现锯齿。

```css
body {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
```

## font-display

有时，样式表指定的字体需要下载（称为 web font），`font-display`属性用于控制浏览器在下载字体时的渲染行为。

```css
@font-face {
  font-family: 'my-font';
  font-display: optional;
  src: url(my-font.woff2) format('woff2');
}
```

这里需要理解，浏览器对于下载字体的处理过程。

首先，浏览器发现样式表指定的字体，是一种需要下载的字体，会去检查缓存里面是否存在这种字体，如果不存在就开始从网上下载。这时，网页上使用这种字体的文字，会显示不出来，而展现一片空白。这段时间称为”阻塞期“（block），每种浏览器的”阻塞期“时间长度不尽相同，Chrome、Firefox 和 Safari 都是3秒，即文字会有3秒钟显示不出来，而 IE 是0秒，即没有阻塞期。

然后，阻塞期结束，如果字体已经下载完成，浏览器就会采用下载的字体进行渲染，文字就会显示出来。如果下载还没有结束，浏览器就会采用替代字体进行渲染，文字也会显示出来，但是与最终状态不一样，这段时间称为”替换期“（swap）。此时，浏览器其实还在下载字体。

最后，等到字体下载成功，这时浏览器会用下载的字体，替换现有的字体，这时网页会一闪。如果字体下载失败了，这时浏览器就会继续使用现有的字体，因此网页不会发生变化。

`font-display`可以取以下值。

（1）`font-display: block`

这是浏览器的默认行为，即打开阻塞期。

（2）`font-display: swap`

这个值会关闭阻塞期，直接进入替换期，即浏览器不会出现文字显示不出来的情况。

（3）`font-display: fallback`

这个值设置阻塞期的长度是100毫秒，即文字有100毫秒显示不出来，然后立即进入替换期。等到字体下载结束，再使用下载的字体渲染。

（4）`font-display: optional`

这个值设置阻塞期也是100毫秒。然后，等到100毫秒结束，浏览器发现字体已经下载完成，就使用下载的字体渲染，否则就不再下载，永久性使用替代字体渲染。它主要用于网速较慢的环境，不让用户长时间等到字体下载。

一般来说，正常情况下都推荐使用`font-display:optional`。如果是图标字体等没有替代字体的情况下，可以使用`font-display: block`。

## 参考链接

- [Font-display](https://font-display.glitch.me/), by Monica Dinculescu
