# CSS 动画

## timer

- linear：线性运行，各个时刻速度都一样。
- ease: 快速加速，然后逐渐减速，CSS 的默认值。
- ease-in：逐渐加速，结尾时变快，适用于退出页面显示的元素。
- ease-out：开始时速度最快，然后逐渐慢下来，适用于进入页面显示的元素。
- ease-in-out：主键加速然后变慢，与`ease`相似，但开始时加速较慢，适合那些在页面有着明确开始和结束的动画。

```css
#div1 {transition-timing-function：linear;} 
#div2 {transition-timing-function：ease;} 
#div3 {transition-timing-function：ease-in;} 
#div4 {transition-timing-function：ease-out ;} 
#div5 {transition-timing-function：ease-in-out;}
```

上面的代码等价于下面的代码。

```css
#div1 {transition-timing-function: cubic-bezier(0,0,1,1);}
#div2 {transition-timing-function: cubic-bezier(0.25,0.1,0.25,1);}
#div3 {transition-timing-function: cubic-bezier(0.42,0,1,1);}
#div4 {transition-timing-function: cubic-bezier(0,0,0.58,1);}
#div5 {transition-timing-function: cubic-bezier(0.42,0,0.58,1);}
```

## transition

`transition`属性定义元素状态变化的过渡。

```css
transition: [*property] [*transition-duration] [transition-timing-function] [transition-delay];
```

`transition`属性一共有四个参数。

- `*property`：元素的哪一个 CSS 属性需要过渡效果，该参数必需。
- `*transition-duration`：过渡效果的持续时间，该参数必需。
- `transition-timing-function`：定时函数，默认是`ease`。
- `transition-delay`：过渡从多少秒以后开始，默认是`0`。

```css
/*1*/ transition: background-color 2s;
/*2*/ transition: background-color 2s 0.5s;
/*3*/ transition: background-color 2s ease-in;
/*4*/ transition: background-color 2s ease-out 0.5s;
/*5*/ transition: background-color 2s, height 1s ease-in-out;
/*6*/ transition: all 1s ease-out;
```

## animation

`animation`属性用来指定元素的动画效果。

```css
animation: [*animation-name] [*animation-duration] [animation-timing-function] [animation-delay] [animation-iteration-count] [animation-direction] [animation-fill-mode] [animation-play-state];
```

- `*animation-name`：关键帧的名字，该参数必需。
- `*animation-duration`：动画持续的时间，该参数必需。
- `animation-timing-function`：定时器函数，默认是`ease`。
- `animation-delay`：动画效果多少秒后开始，默认为`0`。
- `animation-iteration-count`：动画重复的次数，可以指定为一个整数，表示多少次，默认值是`infinite`关键字，表示无限次。
- `animation-direction`：动画方向，可能的值为`forward`、`backward`或`alternating`，默认值为`normal`。
- `animation-fill-mode`：默认值为`none`。
- `animation-play-state`：动画默认是否生效，默认值为`running`。

```css
@keyframes bounce {
  0% {
    transform: scale(0.1);
    opacity: 0;
  }
  60% {
    transform: scale(1.2);
    opacity: 1;
  }
  100% {
    transform: scale(1);
  }
}
.ball {
  animation: bounce 2s infinite;
}
```

### keyframes

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

