# CSS选择器

## 基本选择器

`#elementId`选中指定`id`属性的元素。

`.elementClass`选中指定`class`属性的元素。

## :first-of-type，:last-of-type

`:first-of-type`选中容器里面，第一个符合要求的元素。

```css
p:first-of-type {
  font-size: 1.25em;
}
```

`:last-of-type`选中容器里面，最后一个符合要求的元素。

```css
p:last-of-type {
  font-size: 0.75em;
}
```

## :matches()

`:matches(A, B)`选择器表示匹配A或B。

```css
:matches(.foo, .bar) {
  background-color: green;
}

/* 等同于 */

.foo, .bar {
  background-color: green;
}
```

它可以简化一些选择器的写法。

```css
.syntax-highlighted .css-keyword,
.syntax-highlighted .css-tag {
  color: rgb(170, 13, 145);
}

/* 等同于 */

.syntax-highlighted :matches(.css-keyword, .css-tag) {
  color: rgb(170, 13, 145);
}
```

## :not()

`:not()`表示选中不匹配指定条件的元素。

```css
a:not(.internal) {
  color: red;
}
```

`:not()`可以采用链式写法。

```css
:not(i):not(em)

/* 等同于 */

:not(i, em)
```

## :nth-child()，:nth-last-child()

`:nth-child()`选中指定位置的子元素。`:nth-last-child()`选中倒数位置的子元素。

```css
p:nth-child(2) {
  color: red;
}
```

`:nth-child()`选中第二个子元素，而且这个元素必须是`p`元素。

`:nth-child()`和`:nth-last-child()`可以使用通配符作为参数，参见`:nth-of-type()`部分的说明。

```css
.module:nth-child(4n) {
  margin-right: 0;
}
```

## :nth-of-type()，:nth-last-of-type()

`:nth-of-type()`选中指定类型和指定位置的元素，`:nth-last-of-type()`选中倒数位置的指定类型和指定位置的元素。

```css
p:nth-of-type(2) {
  color: red;
}
```

`:nth-of-type`选中子元素之中的第二个`p`元素。

通配符用法。

```css
li:nth-of-type(2n) {
  background: lightslategrey;
}

li:nth-of-type(3n+2) {
  background: blue;
}
```

`:nth-of-type`的参数可以是`an + b`的形式。

- “a”是一个整数
- “n”作为英文字母，总是不变的，含义是“0, 1, 2, ....”
- “+”作为一个运算符，可以是“+”，也可以是“-”
- “b”是一个整数，如果提供了运算符，就必须提供“b”

`:nth-of-type`的参数还可以是`even`或`odd`。

```css
li::nth-of-type(odd)  {
  background: lightslategrey;
}
```

## BEM命名法

BEM是Block（区块）、Element（元素）、Modifier（修饰符）三者的简称。区块是顶级组件的抽象，元素是组件的组成部分，修饰符是组件或元素的状态。区块与元素之间用两个下划线连接，元素与修饰符之间用两个连词线连接。

```css
/* Block component */
.btn {}

/* Element that depends upon the block */
.btn__price {}

/* Modifier that changes the style of the block */
.btn--orange {}
.btn--big {}
```

对应的HTML代码结构如下。

```html
<a class="btn btn--big btn--orange" href="http://css-tricks.com">
  <span class="btn__price">$9.99</span>
  <span class="btn__text">Subscribe</span>
</a>
```

BEM的重要特点就是CSS是扁平式的，不存在元素嵌套。

## target

target选择器用来匹配当前hash。

产生动画效果。

```css
#further-resources:target {
  animation: highlight .8s ease-out;
}

@keyframes highlight {
  0% { background-color: #FFFF66; }
  100% { background-color: #FFFFFF; }
}
```

弹出效果。

```css
#search-overlay {
  position: fixed;
  top: 1em;
  bottom: 1em;
  right: 1em;
  left: 1em;
  /* … */
  opacity: 0;
  transition: opacity .3s ease-in-out;
  pointer-events: none;
}

#search-overlay:target {
  opacity: 1;
  pointer-events: auto;
  transition: opacity .3s ease-in-out;
}
```

导航栏效果

```css
.main-nav {
  position: fixed;
  top: 0;
  width: 0;
  height: 100%;
  background: #3B3B3B;
  overflow-y: auto;
  transition: width 0.3s ease;
}

#main-nav:target {
  width: 20%;
}

#main-nav:target + .page-wrap {
  width: 80%;
  .open-menu {
     display: none;
  }
  .close-menu {
     display: block;
  }
  .main-header {
    width: 80%;
    left: 20%;
  }
}
```

## 伪元素（Pseudo-element）

伪元素（::before或者::after）是每个元素额外多出来的DOM节点。


```css
.pebble::before {
  ...
}
.pebble::after {
  ...
}

```

伪元素使用两个双引号标识，如果希望IE8支持，也可以使用单引号。

```css

button::after {
  content: '';
  position: absolute;
  top: -50%;
  right: -50%;
  bottom: -50%;
  left: -50%;
  background: linear-gradient(to bottom, rgba(229, 172, 142, 0.1), rgba(255,255,255,0.5) 50%, rgba(229, 172, 142, 0.1));
  transform: rotateZ(60deg) translate(-5em, 7.5em);
}

button:hover::after {
  animation: sheen 1s forwards;
}

@keyframes sheen {
  100% {
    transform: rotateZ(60deg) translate(1em, -9em);
  }
}

```

参考链接

- Donovan Hutchinson, [Animating pseudo-elements](http://cssanimation.rocks/post/pseudo-elements/)

## 伪类

- :empty：没有任何子元素
- :in-range：针对有range属性的input
- :out-of-range：针对有range属性的input
- :optional：没有required属性的input元素
- :required
- :disabled
- :fullscreen
- :not()

