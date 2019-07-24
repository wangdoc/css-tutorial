# 属性选择器

- `[attribute]`	匹配指定属性，不论具体值是什么
- `[attribute="value"]`	完全匹配指定属性值
- `[attribute~="value"]`	属性值是以空格分隔的多个单词，其中有一个完全匹配指定值
- `[attribute|="value"]`	属性值以value-打头
- `[attribute^="value"]`	属性值以value开头，value为完整的单词或单词的一部分
- `[attribute$="value"]`	属性值以value结尾，value为完整的单词或单词的一部分
- `[attribute*="value"]`	属性值为指定值的子字符串

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
