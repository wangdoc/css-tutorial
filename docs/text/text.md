# 文本

## direction

`direction`属性设置块级元素内部的文本阅读方向。

它的默认值是`ltr`（从左到右），适用于大部分语言。它还可以设成`rtl`（从右到左）。

```css
blockquote {
  direction: rtl;
}
```

一般采用 HTML 语言的`dir`属性控制文本阅读方向，而不是使用这个属性。

## text-align

`text-align`属性设置块级元素内部的文本对齐方式。

它可以取以下值。

- left：默认值，文本向左对齐
- right：右对齐
- center：居中对齐
- justify：两端对齐，除了最后一行是左对齐。
- inherit：继承父元素的值
- start：`direction`属性为从左到右时，为左对齐；从右到左时，为右对齐
- end：`direction`属性为从左到右时，为右对齐；从右到左时，为左对齐

## vertical-align

`vertical-align`设置一个元素与在同一条水平线上的其他元素如何对齐。这些元素需要都是`inline`。它可以取以下值。

- baseline：对齐父元素的基线，默认值
- length: 升高或降低特定的长度，可使用负值
- %：升高或降低`line-height`的百分比，不允许负值
- sub：设为下标
- super：设为上标
- top: 当前元素的顶部对齐最高元素的顶边
- text-top：当前元素的顶部对齐父元素字体的顶部
- middle：元素位于父元素的垂直中部
- bottom：当前元素的底部对齐本行最低元素的底部
- text-bottom：当前元素的底部，对齐父元素字体的底部
- initial：设置为默认值
- inherit：继承父元素的值

这个属性通常用于同一行的图标与文字的对齐。

```css
vertical-align: middle;
```

这个命令对设为`display: table-cell`的元素也有效，可以控制元素在单元格之中的垂直对齐方式。这时，一般使用`top`、`middle`和`bottom`等值。

## tab-size

`tab-size`属性设置 Tab 键的宽度，可以设置为整数（表示多少个空格），也可以设置为具体的长度单位。

```css
/* 整数植 */
tab-size: 4;
tab-size: 0;

/* 长度单位 */
tab-size: 10px;
tab-size: 2em;
```

该属性常用于`<pre>`标签之中。

```css
pre {-moz-tab-size: 16;} /* Code for Firefox */
pre {-o-tab-size: 16;} /* Code for Opera 10.6-12.1 */
pre {tab-size: 16;}
```

## word-wrap

`word-wrap`的正式名称是`overflow-wrap`，用于规定是否可以在一个词内部断行，避免溢出容器。

它可以取两个值。

- normal：只在可以断行的地方断行。
- break-word：可以在任意点断行，避免某个词过长，发生溢出。

## word-break

`word-break`用于规定是否可以在词内断行。

它可以取三个值。

- normal：使用浏览器默认的断行规则
- break-all：对于非 CJK 字符，可以任意字符之间断行。
- keep-all：对于 CJK 字符不允许换行。非 CJK 字符与`normal`相同。

## hyphens

浏览器打开连字号功能，需要两个步骤。第一个步骤是设置文本的语言。这将告诉浏览器使用哪个连字词典，正确的自动连字需要一个适合文本语言的连字词典。如果浏览器不知道文本的语言，即使打开 CSS 设置也不会自动连词。

设置网页语言，应该使用`<html>`标签的`lang`属性。

```html
<html lang="en">
```

CSS 里面使用自动连词，要开启`hyphens`属性。`hyphens`属性控制块级元素之中，文本是否显示连词线。

```css
hyphens: auto;
```

`hyphens`属性可以取以下三个值。

（1） none

`none`表示一个词不会在断行处被拆开，即断行处不会有连词线。

（2）manual

`manual`表示只有在一个词内部的字符表示可以有连词线时，才会在断行处拆开。断行处，会有连词线。

两个字符可以表示此处可以断行，并显示连词线，一个是`-`(U+2010)，表示此处可以有一个可见的断行，即使不在此处断行，这里也会有连词线显示；另一个是`U+00AD`，表示不可见的断行，HTML 文档里面可以用`&shy;`插入。

（3）auto

`auto`表示浏览器决定一个词是否可以在断行处拆开，以及是否会有连词线。

## 参考链接

- [All you need to know about hyphenation in CSS](http://clagnut.com/blog/2395), Richard Rutter
