# CSS高级功能

## 自定义属性

CSS 提供的属性（比如`font-weight`、`line-height`）都是标准给定的，但是 CSS 也允许用户自定义属性，这又称为“CSS 变量”。

自定义属性跟普通属性一样，也是定义在某个选择器里面，而且只对该选择器有效。因此自定义属性所在区块，相当于变量的作用域。

`:root`选择器之中，可以设置全局的自定义属性。

```css
:root {
  --base: #ffc600;
  --spacing: 10px;
  --blur: 10px;
}
```

变量也可以在行内定义。

```html
<html style = "--color: red;">
```

所有自定义属性都必须以两个连词线开头，并且大小写敏感。

使用时，通过`var()`函数取出变量。

```css
img {
  padding: var(--spacing);
  background: var(--base);
  -webkit-filter: blur(var(--blur));
  filter: blur(var(--blur));
}
```

`var()`函数接受第二个参数，指定默认值。如果某个自定义属性没有设置，默认值就会生效。

```css
width: var(--custom-width, 20%);
```

下面是另一个例子。

```css
foo {
  padding: var(--gutter, 10px 0 0 5px);
}
```

如果默认值包含逗号，那么`var()`会将第一个逗号后面的所有值，当作默认值。

```css
.someElement {
  font-family: var(--main-font, "lucida grande" , tahoma, Arial);
}
```

上面代码中，`--main-font`的默认值是`"lucida grande" , tahoma, Arial`。

`var()`内部还可以使用`var()`。

```css
.someElement {
  background-color: var(--first-color, var(--second-color, white));
}
```

上面代码中，如果没有设置`--first-color`，默认值`var(--second-color, white)`就会生效。如果`--second-color`也没有设置，那么`white`就会生效。

自定义属性可以是全局的，也可以是局部的。在`:root`选择器里面定义的，就是全局变量，可以在任何其他选择器里面读取。而在其他选择器里面定义，就是局部变量，只能在该选择器里面读取。

下面代码中，局部变量可以覆盖全局变量。

```css
:root { --text-color: green; }
div { --text-color: blue; }
.error { --text-color: red; }

* {
  color: var(--text-color);
}
```

上面代码中，一般文字是绿色，`div`元素的文字是蓝色，`error`类的文字是红色。

定义变量的时候，也可以读取其他变量。

```css
:root {
  --brand-color: red;
  --header-text-color: var(--brand-color);
}
```

变量也可以与`calc`函数结合使用。

```css
:root {
  --container-width: 1000px;
  max-width: calc(var(--container-width) / 2);
}
```

变量不包含单位时，不能直接添加单位。

```css
/* 无效 */
.quote {
  --t-padding: 20;
  padding-top: var(--t-padding)px;
}

/* 有效 */
.quote {
  --t-padding: 20;
  padding-top: calc(var(--t-padding) * 1px);
}
```

JavaScript 可以操作这些变量。

```javascript
element.style.setProperty('--my-color', 'rebeccapurple');
element.style.getPropertyValue('--my-color');
// "rebeccapurple"
element.style.removeProperty('--my-color');
```

下面是例子。

```javascript
// 取得变量值
var styles = window.getComputedStyle(document.documentElement);
var bgValue = String(styles.getPropertyValue('--background')).trim();

// 设置变量值
document.documentElement.style.setProperty('--background', 'black');
// 另一种写法
document.documentElement.style.setProperty('--h-color', 'var(--p-color)');
```

下面是一个监听事件的例子。

```javascript
const docStyle = document.documentElement.style;

document.addEventListener('mousemove', (e) => {
  docStyle.setProperty('--mouse-x', e.clientX);
  docStyle.setProperty('--mouse-y', e.clientY);
});
```

下面是一个使用CSS变量的例子，只要`<input>`的值发生变化，样式就会随之发生变化。

```javascript
// get the inputs
const inputs = [].slice.call(document.querySelectorAll('.controls input'));

// listen for changes
inputs.forEach(input => input.addEventListener('change', handleUpdate));
inputs.forEach(input => input.addEventListener('mousemove', handleUpdate));

function handleUpdate(e) {
  // append 'px' to the end of spacing and blur variables
  const suffix = (this.id === 'base' ? '' : 'px');
  document.documentElement.style.setProperty(`--${this.id}`, this.value + suffix);
}
```

## 参考链接

- [CSS Variables Guide](https://nearsoft.com/blog/css-variables-guide/), Tony Martinez

## supports

`supports`命令用来判断浏览器是否支持某项CSS功能。

```javascript
@supports not (display: grid) {
  // 不支持网格布局
  // 老式浏览器代码
}
@supports (display: grid) {
  // 支持网格布局
  // 新式浏览器代码
}
```

另一个例子。

```javascript
@supports (object-fit: cover) {
  img {
    object-fit: cover;
  }
  div {
    width: auto;
    background: green;
   // some other complex code for the fancy new layout
  }
}
```

## initial-letter

`initial-letter`决定首字母的下沉样式。

```css
/* 默认值 */
initial-letter: normal;

/* 占据1.5行高度 */
initial-letter: 1.5;

/* 占据3行高度 */
initial-letter: 3.0;

/* 占据3行高度，下沉2行高度 */
initial-letter: 3.0 2;
```

## 滤镜

网页的灰度显示。

```css
html {
  -webkit-filter: grayscale(100%);
  filter: grayscale(100%);
}
```

## CSS Shape

`shape-outside`属性使得行内（inline）的内容，围绕`outside`指定的曲线排列。

`shape-margin`属性指定`shape-outside`与内容之间的`margin`。

```css
.circle {
  width: 250px;
  height: 250px;
  background-color: #40a977;
  border-radius: 50%;
  float: left;
  -webkit-shape-outside: circle();
  shape-outside: circle();
}
```

`circle`函数可以使用`circle(r at x y)`这样的形式，定义半径和圆心的坐标。注意，这里的坐标是相对于原始形状，而不是相对于父容器。

其他形状的函数。

- ellipse()
- polygon()

参考链接

- [How to Use CSS Shapes in Your Web Design](https://webdesign.tutsplus.com/tutorials/how-to-use-css-shapes-in-your-web-design--cms-27498), by Louie R.
