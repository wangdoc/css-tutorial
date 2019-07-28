# 字体

## 字体文件类型

内嵌OpenType（Embedded OpenType，.eot）。在使用@font-face时，Internet Explorer 8及之前的版本仅支持内嵌OpenType。内嵌OpenType是Microsoft的一项专有格式，它使用数字版权管理技术防止在未经许可的情况下使用字体。

TrueType（.ttf）和OpenType（.otf），台式机使用的标准字体文件类型。TrueType和OpenType得到了Mozilla Firefox（3.5及之后的版本）、Opera（10及之后的版本）、Safari（3.1及之后的版本）、Mobile Safari（iOS 4.2及之后的版本）、Google Chrome（4.0及之后的版本）及Internet Explorer（9及之后的版本）的广泛支持。这些格式不使用数字版权管理。

Web开放字体格式（Web Open Font Format，.woff）。这种较新的标准是专为Web字体设计的。Web开放字体格式的字体是经压缩的TrueType字体或OpenType字体。WOFF格式还允许在文件上附加额外的元数据。字体设计人员或厂商可以利用这些元数据，在原字体信息的基础上，添加额外的许可证或其他信息。这些元数据不会以任何方式影响字体的表现，但经用户请求，这些元数据可以呈现出来。Mozilla Firefox（3.6及之后的版本）、Opera（11.1及之后的版本）、Safari（5.1及之后的版本）、Google Chrome（6.0及之后的版本）及Internet Explorer（9及之后的版本）均支持Web开放字体格式。

可缩放矢量图形（Scalable Vector Graphics，.svg）。简言之，应避免对Web字体文件使用SVG。它更多地用于早期Web字体，因为它是iOS 4.1上移动Safari唯一支持的格式（还有可能引起一些崩溃的情况）。从iOS 4.2（于2011年初即被广泛使用）起，移动Safari开始支持TrueType。

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
