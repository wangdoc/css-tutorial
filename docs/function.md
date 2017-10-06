# 函数

CSS 提供一些函数，方便操作。

## minmax

`minmax`提供一个长度范围，不小于较小值，不大于较大值。

```css
minmax( min, max )
```

如果第二个参数`max`小于第一个参数`min`，那么`max`会被忽略，等同于将长度设置为`min`。

```css
minmax(400px, 50%)
minmax(30%, 300px)
```

网格布局中，`max`也允许设置为比例因子`fr`，但`min`不能设置为`fr`。

```css
minmax(200px, 1fr)
```

网格布局中，还可以使用关键字`max-content`和`min-content`，分别表示最大的和最小的可分配宽度。

```css
minmax(100px, max-content)
minmax(min-content, 400px)
```

关键字`auto`在`max`位置等同于`max-content`，在`min`位置等同于`min-content`。

```css
minmax(max-content, auto)
minmax(auto, 300px)
minmax(min-content, auto)
```

## image-set()

`image-set()`用来选取符合响应式条件的图片。

```css
background-image: image-set( "foo.png" 1x, "foo-2x.png" 2x);
```
