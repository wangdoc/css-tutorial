# CSS 计数器

## 简介

- counter-reset：新建或重置一个计数器。
- counter-increment：指定计数器的值加1。
- counter()：取出指定计数器的值。

```css
counter-reset：counterName;
counter-increment: counterName;
counter(counterName);
```

下面是一个例子。

```css
ul{
  counter-reset: section;
}
li{
  list-style-type: none;
  counter-increment: section;
}
li:before{
  content: counters(section, '-') '.';
}
```

## counter-reset

`counter-reset`属性新建或重置计数器。计数器的值默认为`0`。

可以使用第二个参数，修改计数器的默认值。

```css
counter-reset: count -1;
```

上面示例将计数器的默认值设为`-1`。

可以在一条语句里面，同时新建多个计数器。

```css
counter-reset: counter1 1 counter2 4;
counter-reset: chapter section 1 page;
```

上面示例，第一行新建了两个计数器，第二行新建了三个计数器，并且计数器`section`的默认值设为`1`。

如果这个属性的值设为`none`，则表示不重置计数器，可以用来取消上层规则的设置。

## counter-increment

`counter-increment`属性默认将计数器的值加`1`，但也可以使用第二个值，指定变化的幅度。

```css
counter-increment: counter-name -1;
```

上面示例表示将计数器的值减`1`。

可以在一条`counter-increment`语句里面，同时改变多个计数器。

```css
counter-increment: counter1 1 counter2 -4;

counter-increment: chapter section 2 page;
```

上面示例的第一行，计数器`counter1`增加`1`，计数器`counter2`减去`4`。第二行，计数器`chapter`和`page`增加`1`，计数器`section`增加2。

如果这个属性设为`none`，表示不改变计数器的值。

## counter()

`counter()`还有可选的第二个参数，设置计数器的值样式，默认是阿拉伯数字。

```css
counter(countername, upper-roman)；
```

上面示例将计数器的值样式设为大写的罗马数字。

常用的样式值如下。

- decimal-leading-zero：数字带有前导0。
- lower-roman：小写的罗马数字。
- upper-roman：大写的罗马数字。
- lower-alpha：小写的英文字母。
- upper-alpha：大写的英文字母。

也可以使用`@counter-style`定义自己的规则。

```css
@counter-style winners-list {
  system: fixed;
  symbols: url(gold-medal.svg) url(silver-medal.svg) url(bronze-medal.svg);
  suffix: " ";
}
```

上面示例是金牌、银牌、铜牌的计数符号。

```css
@counter-style thumbs {
  system: cyclic;
  symbols: "\1F44D";
  suffix: " ";
}

ul {
  list-style: thumbs;
}
```

上面示例是将列表符号变成点赞。

```css
@counter-style circled-alpha {
  system: fixed;
  symbols: Ⓐ Ⓑ Ⓒ Ⓓ Ⓔ Ⓕ Ⓖ Ⓗ Ⓘ Ⓙ Ⓚ Ⓛ Ⓜ Ⓝ Ⓞ Ⓟ Ⓠ Ⓡ Ⓢ Ⓣ Ⓤ Ⓥ Ⓦ Ⓧ Ⓨ Ⓩ;
  suffix: " ";
}

.items {
  list-style: circled-alpha;
}
```

上面示例将列表符号变成带圈的英文字母。

## counters()

`counters()`用来取出计数器的值，并且指定多重计数器之间的连接字符。

```css
counters(name, strings, style);
```

它与`counter()`的不同是多了一个`strings`参数，表示子序号的连接字符串。

```css
counters(countername, '-');
counters(countername, '.', upper-roman);
```

上面示例第一行中，计数器与子计数器的连接符号为`-`。第二行为小数点。
