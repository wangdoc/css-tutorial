# text-decoration

文本可以附加装饰线（比如下划线），以下属性用来设置装饰线。

## text-decoration

`text-decoration`设置文本采用哪一种装饰线，主要有下划线（underline）、上划线（overline）和删除线（line-through）等类型。

```css
h3 {
  text-decoration: underline;
}
```

该属性可以取以下值。

- none：没有任何修饰
- underline：下划线，默认线宽`1px`
- overline：上划线，默认线宽`1px`
- line-through：删除线，默认线宽`1px`
- inherit：继承父元素的设置

多种装饰线可以同时存在。

```css
.multiple {
  text-decoration: underline overline line-through;
}
```

默认情况下，装饰线的颜色与文本的`color`属性一致。`text-decoration-color`属性可以修改颜色。

`text-decoration`属性还可以用作`text-decoration-style`和`text-decoration-color`的简写形式。

```css
.fancy-underline {
  text-decoration-line: underline;
  text-decoration-style: wavy;
  text-decoration-color: red;

  /* 等同于 */
  text-decoration: underline wavy red;
}
```

## text-decoration-color

`text-decoration-color`设置文本的装饰线的颜色。

```css
a {
  text-decoration-color: #E18728;
}
```

## text-decoration-style

`text-decoration-style`设置文本的下划线（underline）、上划线（overline）和删除线（line-through）的样式。

```css
a {
  text-decoration-style: solid;
}
```

该属性支持以下样式。

- solid：单条直线
- double：双条直线
- dotted：多个点组成的直线
- dashed：多个短划线组成的直线
- wavy：波浪线

## text-decoration-line

`text-decoration-line`设置文本采用何种装饰线，与`text-decoration`单个值的写法相同。建议采用后者，因为浏览器的支持度更好。

```css
p {
  text-decoration-line: underline;
}
```

它的取值参考`text-decoration`。

## text-decoration-skip

`text-decoration-skip`设置文本的装饰线应该在哪里中断，主要用于改善文本被装饰以后的可读性。

```css
a {
  text-decoration-skip: ink;
}
```

上面代码中，下划线遇到英语字母`y`和`p`会中断，让它们较长的下划会更清晰地显示出来。

该属性可以取以下值。

- objects：默认值，装饰线遇到图片或其他`inline-block`对象时中断。
- none：装饰线不会有任何中断，包括遇到行内对象。
- spaces：装饰线在空格、断词处中断。
- ink：装饰线遇到有笔画下降或上升的字母时中断。
- edges：装饰线在内容开始后和结束前都收缩一点，主要用于多个连续的装饰线，可以看上去连成一条。
- box-decoration：装饰线在继承的 margin、border 和 padding 处中断。

## 参考链接

- [text-decoration](https://css-tricks.com/almanac/properties/t/text-decoration/), by Sara Cope
- [text-decoration-skip](https://css-tricks.com/almanac/properties/t/text-decoration-skip/), by Marie Mosley

