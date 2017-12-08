# CSS 动画

## 基本用法

首先，需要使用`keyframes`定义一个动画。

```css
keyframes rotation {
  from {
    transform: rotate(90deg);
  }
  to {
    transform: rotate(450deg);
  }
}
```

上面代码中，`keyframes`关键字后面是动画名称（上例是`rotation`），大括号内部是关键帧，`from`表示起始帧，`to`表示结束帧，其他帧由浏览器自动计算出来。

另一种定义方法是使用百分比，定义关键帧，`from`就是`0%`，`to`就是`100%`。

```css
@keyframes color {
  0% {
    fill: #99002f
  }
  50% {
    fill: #ffc426
  }
  100% {
    fill: #99002f
  }
}
```

使用的时候，通过`animation`属性将动画赋给指定元素即可。（[Demo](http://demo.hongkiat.com/css3-animation-steps/)）

```css
.second {
  animation: rotation 60s steps(60) infinite;
  transform-origin: 100% 50%;
}
```

`animation`属性是一个简写形式，它包括以下一些子属性。

- animation-name
- animation-duration
- animation-timing-function
- animation-delay
- animation-iteration-count
- animation-direction
- animation-fill-mode

```css
svg path {
  animation: color 2s infinite cubic-bezier(.85,.01,.25,1);
}

/* 等同于 */
svg path {
  animation-name: color;
  animation-duration: 2s;
  animation-iteration-count: infinite;
  animation-timing-function: cubic-bezier(.85,.01,.25,1);
}
```

## 隐入（fade in）

```css
@keyframes fade-in {
  0% { opacity: 0; }
  100% { opacity: 1; }
}
.fade-in {
  animation: fade-in 1s forwards linear;
}
```

## 上浮（fade up）

```css
@keyframes fade-up {
  0% {
    opacity: 0; transform: translateY(3em);
  }
  100% {
    opacity: 1; transform: translateY(none);
  }
}
.fade-up {
  animation: fade-up 3s cubic-bezier(.05,.98,.17,.97) forwards;
}
```

## 左右摆动（wiggle）

```css
@keyframes wiggle {
0%, 7% { transform: rotateZ(0); opacity: 0; }
15% { transform: rotateZ(-15deg); opacity: 1; }
20% { transform: rotateZ(10deg); }
25% { transform: rotateZ(-10deg); }
30% { transform: rotateZ(6deg); }
35% { transform: rotateZ(-4deg); }
40%, 100% { transform: rotateZ(0); }
}
```

## 上下弹跳（bounceAround）

```css
.animation {
	…
	animation: bounceAround 1.1s ease-in-out infinite;
}

@keyframes bounceAround {
	0% {transform:translateY(0);}
	20% {transform:translateY(-60px) rotate(0deg);}
	25%{transform:translateY(20px) rotate(0deg);}
	35%, 55%{transform:translateY(0px) rotate(0deg);}
	60% {transform: translateY(-20px) rotate(0deg);}
	100%{transform: translateY(-20px) rotate(360deg);}
}
```

