# CSS的单位

## inherit

大多数 CSS 属性默认继承它的父元素的设定，但是有一些属性默认不继承。比如，`input`元素和`textarea`元素的 CSS 属性，都是不继承父元素的。这时，可以强制它们继承。

```css
* {
  font-family: inherit;
  line-height: inherit;
  color: inherit;
}

html {
  font-size: 125%;
  font-family: sans-serif;
  line-height: 1.5;
  color: #222;
}
```

上面代码中，首先强制所有元素的`font-family`、`line-height`和`color`属性都继承父元素，然后在网页的根元素`html`上设置具体的值。

## em

`em`是一种相对单位，`1em`等于当前元素的`font-size`。一般来说，浏览器默认的字体大小是16像素，所以`1em`默认等于16像素。

```css
h1 { font-size: 20px } /* 1em = 20px */
p { font-size: 16px } /* 1em = 16px */
```

上面代码中，对于`h1`元素，`1em`相当于`20px`；对于`p`元素，`1em`相当于`16px`。

如果当前元素没有指定字体的像素大小，那么`1em`等于父元素字体的像素大小。这一点非常重要，务必牢记。

```css
html { font-size: 16px }
h1 { font-size: 2em } /* 16px * 2 = 32px */
```

上面代码中，`h1`元素的字体大小是`2em`，但是它没有指定像素字体大小，因此`2em`等于2倍的父元素像素字体大小，也就是`32px`。

`em`的一大好处是，很容易保持不同元素之间的比例关系，因此它比像素单位更合适用来设定字体大小。

```css
html { font-size: 100%; }
h1 { font-size: 2em; }
p { font-size: 1em; }
```

上面代码中，`h1`的字体大小就是`p`的2倍。

整个网页的字体大小，如果全部使用`em`单位，不使用像素单位，会引发一个问题。`em`将会基于父元素计算，从而出现累积效应。

```css
html { font-size: 100%; } /* 默认是 16px */
div { font-size: 2em; } /* 字体大小 32px */
p { font-size: 1em; } /* 字体大小 32px */
```

上面代码中，`html`是`div`的父元素，所以`div`的`1em`是基于`html`计算的，因此`2em`字体大小等于`32px`。另一方面，`div`是`p`的父元素，所以`p`的`1em`实际上也是`32px`。

除了字体大小，其他许多属性也可以使用`em`，比如`margin`和`padding`，相当于间接由`font-size`决定。

```css
.header {
  font-size: 16px;
  padding: 0.5em 0.75em; /* 相当于 8px 12px */
  background: #7F7CFF;
}
```

上面代码中，`.header`元素的字体大小是`16px`，因此`1em`等于`16px`，所以`padding`就相当于`8px 12px`。

这里比较混淆的是，如果`font-size`也使用`em`，两者的计算基点是不一样的。

```css
h1 {
  font-size: 2em; /* 1em = 16px */
  padding： 1em;  /* 1em = 32px */
}
```

上面代码中，`font-size`是基于父元素计算的，如果父元素的字体大小是`16px`，那么`font-size`就是`32px`；`padding`是基于`font-size`计算的，由于`h1`的`font-size`是`32px`，所以`padding`就是`32px`。

由于以上的累积效应和计算基点差异的原因，造成`em`不容易精确控制，实际开发中往往改用`rem`。

## rem

`rem`单位与`em`几乎完全一致，只有一个差异，它总是等于根元素`<html>`的`font-size`大小，与当前元素或父元素的设置无关，这就避免了`em`的缺陷。

```css
h1 {
  font-size: 2rem; /* 1rem = 16px */
  margin-bottom: 1rem;
}

p {
  font-size: 1rem; /* 1rem = 16px */
  margin-bottom: 1rem;
}
```

上面代码中，不管`<h1>`和`<p>`在什么位置，`1rem`的大小总是不变的。

那么，何时使用`rem`，何时使用`em`呢？一个[规则](https://zellwk.com/blog/rem-vs-em/)是字体大小`font-size`属性使用`rem`，其他必须等比例缩放的属性使用`em`。下面是一个例子。

```css
button {
  font-size: 0.875rem;
  padding: .5em 1em;
  border: .125em solid #e3e3e3;
  @media (min-width: 48rem){ /* min-width: 768px */
    font-size: 1.125rem;
  }
  @media (min-width: 62rem){ /* min-width: 992px */
    font-size: 1.375rem;
  }
}
```

上面代码中，随着屏幕宽度的变化，字体大小会跟着改变，`padding`和`border`会始终保持比例关系。

## vh，vw

`vh`表示百分之一的浏览器视口高度，`vw`表示百分之一的浏览器视口宽度。每当视口的高度和宽度发生变化，它们就会自动重新计算。

```css
html { font-size: 3vw; }
```

上面代码中，如果视口宽度增加，字体大小也会增加；视口宽度减小，字体大小也会减小。但是，如果宽度太小（比如`320px`），这样算出来的字体会太小（`3px`）；如果宽度太大（比如`1440px`），字体又会太大（`43px`）。因此，可以考虑使用`calc`函数。

```css
html { font-size: calc(18px + 0.25vw); }
```

## vmin，vmax

`vmin`表示`vh`与`vw`之中较短的那个单位，`vmax`则表示较长的那个单位。

一般来说，PC的屏幕是屏宽大于屏高，手机的屏幕是屏高大于屏宽。所以，很可能会出现，某一个区域在PC屏幕中宽度较小，在手机屏幕中宽度较大。这时，这两个单位就可以派上用处了。

```css
h1 {
  font-size: 20vmin;
}
```

注意，上面的`h1`使用`vmin`单位时，当宽屏设备的视口宽度缩小时，它的字体大小是不变的，因为视口的高度没有改变。

## ch

`ch`表示多少个字符。

```css
width: 40ch;
```

上面代码表示宽度为40个字符。

## calc()

calc方法用于计算值，常用于两种不同的单位之间的计算（比如百分比和绝对长度）。

实例1。每行放置4张图片，可以采用如下的代码。

```css
img {
  float: left;
  width: calc(25% - 20px);
  margin: 10px;
}
```

实例2。动态排列图片，可以配合media query。

```css

img {
  float: left;
  margin: 10px;
  width: calc(100% * 1 / 4 - 20px);
}

@media (max-width: 900px) {
  img {
    width: calc(100% * 1 / 3 - 20px);
  }
}

@media (max-width: 600px) {
  img {
    width: calc(100% * 1 / 2 - 20px);
  }
}

@media (max-width: 400px) {
  img {
    width: calc(100% - 20px);
  }
}

```

## attr()

attr()用于读取网页元素的属性值。

```css
div[data-line]:after { 
	content: "[line " attr(data-line) "]"; 
}
```

## 参考链接

- Zell, [REM vs EM – The Great Debate](http://zellwk.com/blog/rem-vs-em/)
