# 选择器

选择器决定了样式规则对哪些元素有效。

## 基本选择器

元素名称选择器，选中所有该标签的元素。

`#elementId`选中指定`id`属性的元素。

`.elementClass`选中指定`class`属性的元素。

应该尽量使用 class 选择器，而不是 ID 选择器。

ID 选择器的样式不能在其他元素上复用（记住，在一个页面中，一个id只能出现在一个元素上）。这会导致在其他元素上重复样式，而不是通过class共享样式。

ID 选择器的特殊性比class选择器要强得多。这意味着如果要覆盖使用id选择器定义的样式，就要编写特殊性更强的CSS规则。如果数量不多，可能还不难管理。如果处理规模较大的网站，其CSS就会变得比实际所需的更长、更复杂。

## 通配符选择器

通配符`*`（星号）匹配任何元素。

因为匹配范围太广，会让浏览器加载页面变慢，因此应该谨慎使用通配符。实际适合使用通配符的情况比较少。

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

## 优先级

一个网页元素，可以被多个选择器匹配。如果这些选择器都设置了同样的规则，就有一个”优先级“的问题：到底哪个选择器的优先级更高？

规则是针对性越强的选择器，优先级越高。浏览器会计算每条规则的优先级值，然后采用值最高的规则，计算方法如下。

- `!important`后缀为 10000
- 行内样式为 1000
- ID 为 100
- class、伪类、属性选择器为 10
- 标签名、伪元素为 1

然后，累加得到的分数，哪条规则得分最高，就采用哪条规则。如果得分相同，就采用位置靠后的位置。

下面是一些例子。

- `<li style="color: red;">`：行内样式，得分为1000。
- `ul#nav li.active a`：一个 ID、一个 Class、三个标签名，得分为113。
- `body.ie7 .col_3 h2 ~ h3`：两个 Class，三个标签名，得分为23。
- `#footer *:not(nav) li`：一个 ID、两个标签名，得分为102。注意，`*`没有分数，而且`:not`不算伪类，只计算它括号里面的标签名。
- `ul > li ul li ol li:first-letter`：七个标签名，得分为7。注意，`:first-letter`算作伪元素。
