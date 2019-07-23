# CSS 概述

## 简介

CSS 用于定义网页的样式，比如每个网页元素的位置、大小、颜色等等。

CSS 随着网页的诞生而诞生。1996年12月，CSS 1.0 标准问世，目前广泛使用的是2000年4月发布的 CSS 3 标准。

CSS 3 采用模块化结构，每个模块都是独立定义的，定义完成以后，再加入 CSS 标准。截止2017年，CSS 共有88个模块，下面是其中一次主要模块。

> - Display
> - Box alignment
> - Flexible box
> - CSS Grid
> - Inline Layout
> - Position Layout
> - CSS Shapes
> - CSS Transforms

CSS 样式表就是一个文本文件，定义每个网页元素的样式规则。

## 样式规则

CSS 样式表由大量样式规则组成。每条样式规则分成两个部分：选择器（selector）和声明块（declaration block）。

选择器指明本条规则对哪些网页元素生效，声明块描述样式规则的具体内容。

```css
h1 {
  color: red;
}
```

上面代码是一条样式规则，其中`h1`是选择器，大括号的部分就是声明块。这个规则的意思是，`h1`元素的颜色为红色。

声明块的内容，放在一对大括号里面。大括号之中是一个或多个键值对，每个键值对用分号结尾，给出一条样式描述。键值对的顺序并不重要。

```css
h1 {
  background-color: yellow;
  color: red;
}
```

上面代码中，声明块里面包含两条样式描述，它们的顺序不重要，完全可以对调位置。

声明块可以写成多行，也可以写成一行。缩进和换行只是为了增加可读性，CSS 引擎会忽略它们。

```css
h1 { color: red; }
```

上面代码中，声明块写成了一行。它与写成多行的效果是一样的。

CSS 允许重复声明某个样式，这时最后声明的键值对会覆盖前面的键值对。

```css
h1 {
  color: red;
  color: black;
}
```

上面代码中，颜色属性申明了两次。后面声明的黑色，会覆盖前面声明的红色。

声明块里面的键值对，由键名和键值组成。键名称为 CSS 属性（property），由 CSS 标准给出，键值是该属性允许被赋予的一个值。

学习 CSS，主要就是学习各种各样的 CSS 属性。

## CSS 注释

CSS 使用`/* ... */`表示注释，可以是单行，也可以是多行。

```css
h1 { /* 这是单行注释 */
  color: red;
}

/* 这是多行注释
h1 {
  color: red;
}
*/
```

上面代码中，多行注释包含整个`h1`的样式规则，这意味着这个样式规则不会生效。

注意：注释不能嵌套。

## CSS 的继承

某些 CSS 属性不仅影响网页元素本身，还会影响该元素的后代元素，这称为 CSS 的继承。

最典型的例子就是字体属性`font-family`，网页根元素`html`设置了字体以后，该网页的所有元素都会默认使用指定的字体。

以下是常见的可以继承的 CSS 属性。

> 文本
> - color（颜色，a元素除外）
> - direction（方向）
> - font（字体）
> - font-family（字体系列）
> - font-size（字体大小）
> - font-style（用于设置斜体）
> - font-variant（用于设置小型大写字母）
> - font-weight（用于设置粗体）
> - letter-spacing（字母间距）
> - line-height（行高）
> - text-align（用于设置对齐方式）
> - text-indent（用于设置首行缩进）
> - text-transform（用于修改大小写）
> - visibility（可见性）
> - white-space（用于指定如何处理空格）
> - word-spacing（字间距）
>
> 列表
> - list-style（列表样式）
> - list-style-image（用于为列表指定定制的标记）
> - list-style-position（用于确定列表标记的位置）
> - list-style-type（用于设置列表的标记）
>
> 表格
> - border-collapse（用于控制表格相邻单元格的边框是否合并为单一边框）
> - border-spacing（用于指定表格边框之间的空隙大小）
> - caption-side（用于设置表格标题的位置）
> - empty-cells（用于设置是否显示表格中的空单元格）
>
> 页面设置（对于印刷物）
> - orphans（用于设置当元素内部发生分页时在页面底部需要保留的最少行数）
> - page-break-inside（用于设置元素内部的分页方式）
> - widows（用于设置当元素内部发生分页时在页面顶部需要保留的最少行数）
>
> 其他
> - cursor（鼠标指针）
> - quotes（用于指定引号样式）

## 样式的优先级

如果多条规则都对同一个网页元素指定样式，只要 CSS 属性不发生冲突，那么这些规则都是有效的。

如果 CSS 属性发生冲突，那就存在一个优先级的问题：哪一条规则优先生效？

CSS 采用以下规则，决定样式规则的优先级。

- 特殊性（specificity）
- 顺序（order）
- 重要性（importance）

特殊性指的是选择器的具体程度，选择器越特殊，规则就越强。遇到冲突时，优先应用特殊性强的规则。特殊性最低的是元素名本身，然后是元素的`class`属性，特殊性最高的是`id`属性。建议在样式表中多使用`class`选择器，避免使用`id`选择器，这样的灵活性最好。

规则指的是，同样特殊性的规则，晚出现的优先级高。

重要性指的是，特别注明某条规则的重要程度要比其他所有规则高，方法是在声明的末尾加上`!important`。由于可维护性很差，一旦出现问题，很难排查，除非是殊情况，否则不推荐使用这种方法。

```html
p {
  color: orange !important;
}
```

## 样式表嵌入网页的方法

HTML 网页采用`<link>`标签将 CSS 样式表嵌入网页。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <title>Demo</title>
    <link rel="stylesheet" href="style.css" />
</head>
<body>
  ... ...
</body>
</html>
```

上面代码中，`<link>`标签放在`<head>`内部，`rel="stylesheet"`指明这是样式表，`href`属性给出样式表文件的网址。浏览器解析到这一行代码，就会去加载样式表。

上例的样式表文件是`style.css`。样式表的后缀名通常是`.css`，但也可以是其他后缀名。

网页也可以使用`<style>`标签，直接包含样式规则。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <title>Demo</title>
    <style>
    img {
        border: 4px solid red;
    }
    </style>
</head>
<body>
  ... ...
</body>
</html>
```

上面代码中，`<head>`内部的`<style>`标签直接包含了样式规则。

最后，针对某个网页元素的样式，也可以写在该元素的`style`属性。

```html
<img src="demo.jpg" style="border: 4px solid red;">
```

上面代码中，`style`属性指定了`img`元素的样式。

`style`属性只对当前元素生效，需要一个个指定，非常麻烦。由于多个样式表可以同时对一个元素生效，`style`属性维护起来非也常困难，所以不建议使用，一般只用于 JavaScript 脚本指定动态样式，以及某些特殊情况。

内联样式由于位于外部样式表和嵌入样式表之后，优先级高于其他所有样式，除非其他地方与之冲突的样式标记了`!important`。
