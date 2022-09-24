# 定时器

## `setTimeout`

将函数推迟到一段时间间隔之后再执行

```js
// 语法
let timeId = setTimeOut(fun | code,[delay],[arg1],[arg2],...)
```

- `fun | code`想要执行的函数或代码字符串
- 一般传入的都是函数，由于某些历史原因，支持传入代码字符串，但是不建议这样做
- delay：执行前的延时，以毫秒为单位，默认值是0
- `arg1,arg2...`:要传入被执行函数（或代码字符串）的参数列表

## `clearTimeOut`

取消`setTimeout`的定时器

`setTimeout`在调用时会返回一个定时器表示符（`timer indentifier`)，我们可以使用它来取消执行

```js
var timeId = setTimeOut(function(name,age){
    console.log('定时器',name,age)
},2000,'abc',18)
clearTimeOut(timeId)
```

## `setInterval`

重复运行一个函数，从一段时间间隔之后开始执行，之后以该时间间隔连续重复运行该函数

```js
// 语法
let timeId = setInterval(fun | code,[delay],[arg1],[arg2],...)
```

语法与`setTimeOut`相同，所有参数的意义也是相同的

不过与`setTimeOut`只执行一次不同，`setInterval`是每间隔给定的时间周期性执行

## `clearInterval`

取消`setInterVal`定时器

`setInterVal`在调用时会返回一个定时器表示符（`timer indentifier`)，我们可以通过`setInterVal`来取消这个定时器

```js
var timeId = setInterVal(function(name,age){
    console.log('定时器',name,age)
},2000,'abc',18)
clearInterval(timeId)
```

