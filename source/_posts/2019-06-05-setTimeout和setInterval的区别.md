---
title: setTimeout和setInterval的区别
tags: '-javaScript'
abbrlink: 64e435bc
date: 2019-06-05 18:55:13
---
> 我们再前端开发中需要实现定时任务或者`js`动画，都要用到`setTimeout`和`setInterval`z这两个函数，但是对于他们的原理，如果不清楚，往往会造成一些意想不到的问题。

### `setTimeout`

`setTimeout`方法设置一个定时器，该定时器在定时器到期后执行一个函数或指定的一段代码。

 语法

```javascript
var id = setTimeout(function[,delay,param1...])
var id = setTimeout(function[,delay])
var id = setTimeout(code[,delay])
```

#### 参数

`function`

[`function`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/function) 是你想要在到期时间(`delay`毫秒)之后执行的[函数](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Function)。

`code`

这是一个可选语法，你可以使用字符串而不是[`function`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/function) ，在`delay`毫秒之后编译和执行字符串 (使用该语法是**不推荐的,** 原因和使用 [`eval()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/eval)一样，有安全风险)。

`delay `可选

延迟的毫秒数 (一秒等于1000毫秒)，函数的调用会在该延迟之后发生。如果省略该参数，delay取默认值0，意味着“马上”执行，或者尽快执行。不管是哪种情况，实际的延迟时间可能会比期待的(delay毫秒数) 值长，原因请查看[Reasons for delays longer than specified](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/setTimeout#Reasons_for_delays_longer_than_specified)。

`param1, ..., paramN` 可选

附加参数，一旦定时器到期，它们会作为参数传递给[`function`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/function) 

#### 返回值

返回值`timeoutID`是一个正整数，表示定时器的编号。这个值可以传递给[`clearTimeout()`](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowOrWorkerGlobalScope/clearTimeout)来取消该定时器。

#### 用途

举个例子，三秒后跳转新页面

```javascript
setTimeout(function() {
    location.href = "url"
},3000)
```

------
未完待续。。。





