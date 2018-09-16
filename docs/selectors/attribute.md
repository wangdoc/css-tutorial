# 属性选择器

## 修饰符

属性修饰器支持`i`修饰符，表示不区分大小写。

```css
[class=foo i] {
  color: red;
}
```

上面代码中，属性名`foo`后面的`i`，表示不区分`foo`的大小写，所以下面几个 class 都会匹配。

```html
<div class="foo">...</div>
<div class="Foo">...</div>
<div class="fOo">...</div>
```

这个修饰符对于匹配用户的输入，非常有用。

```css
/**
 * 匹配：
 * <input value="hello world">
 * <input value="hello World">
 * <input value="hElLo WoRlD">
 * ...
 */
[value="hello world" i] { /* ... */ }
```

## 参考链接

- [The CSS attribute selector has a case-insensitive mode](https://www.stefanjudis.com/today-i-learned/the-css-attribute-selector-has-a-case-insensitive-mode/)
