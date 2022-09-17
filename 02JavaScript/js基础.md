# JavaScript

## 认识JavaScript引擎

### 为什么需要JavaScript引擎呢

- 高级的编程语言都是需要转成最终的机器指令来执行的
- 事实上我们编写的JavaScript无论你交给浏览器或者node执行，最后都是需要被cpu执行的
- 但是cpu只认识自己的指令集，实际上市机器语言，才能被cpu执行
- 所以我们需要JavaScript引擎帮助我们将JavaScript翻译成cpu来执行

## 比较常见的JavaScript引擎

- SpiderMonkey：第一框JavaScript引擎，由Brendan Eich （JavaScript作者）开发
- Chakra：微软开发，用于IE浏览器
- JavaScriptCore：webkit中的JavaScript引擎，Apple公司开发
- V8：Google开发的强大JavaScript引擎

## 浏览器内核和js引擎的关系

这里以webkit为例，webkit事实上由两部分组成

- WebCore:负责HTML解析、布局、渲染等相关工作
- JavaScriptCore：解析、执行JavaScript代码

小程序中也是这样划分的

在小程序中编写的JavaScript代码就是被JSCore执行的

## vscode插件配置

1、ES7+React/Redux/React-Native snippets

2、起始位置的光标提示配置

```json
// 在setting.json里面加两个配置
  "editor.bracketPairColorization.enabled": true,
  "editor.guides.bracketPairs": "active",
```

## JavaScript的数据类型

7种原始类型1种复杂类型

原始类型

- Number
- String
- Boolean
- Undefined
- Null
- Bigint
- Symbol

### string

#### 字符串中的转义字符

除了普通的可打印字符以外，一些有特殊功能的字符可以通过转义字符的形式放入字符串中

![image-20220915211024173](C:\Users\10244\AppData\Roaming\Typora\typora-user-images\image-20220915211024173.png)

### Boolean

Boolean类型仅包含两个值：true 和 false

### undefined

undefined类型只有一个值，就是特殊值**undefined**

如果我们声明一个变量，但没有对其进行初始化，它默认就是undefined

注意事项

- 最好在变量定义的时候进行初始化，而不是只声明一个变量
- 不要显示的将一个变量赋值为undefined 

  如果变量刚开始什么都没有，我们可以初始化为0、空字符串、null等值

### null类型

null类型只有一个值，即null

null类型通常用来表示一个对象为空，所以通常我们在给一个对象进行初始化时，会赋值null

#### null和 undefined的关系

- undefined通常只有在一个变量声明但是未初始化时，它的默认值是undefined才会用到
- 并且我们不推荐直接给一个变量赋值为undefined，所以很少主动使用
- null值非常常用，当一个变量保存一个对象，但是这个对象不确定时，我们可以先赋值为null

复杂类型

- Object

### Object

- Object类型是一个特殊的类型，我们通常把它称为引用类型或者复杂类型
- 其他的数据类型我们通常称之为“原始类型”。因为他们的值只包含一个单独的内容（字符串、数字或其他）
- Object往往可以表示一组数据。是其他数据的一个集合
- 在JavaScript中我们可以使用花括号{}的方式来表示一个对象

### 数据类型的转换

#### 字符串string的转换

方式一：隐式转换

一个字符串和另一个字符串进行+操作;

​    如果+运算符左右两边有一个是字符串，那么另一边会自动转换成字符串类型进行拼接

某些函数的执行也会自动将参数转换为字符串类型，比如console.log()

方法二：显示转换

调用String()函数

调用toString()方法

#### 数字类型的Number的转换

转换方式一：隐式转换

在算术运算中，通常会将其他类型转换成数字类型来进行运算 

比如“6” / "2"

但是如果是+运算，并且其中一边有字符串，那么还是按照字符串来拼接的

转换方式二：显示转换

使用Number()函数

其他类型转换数字的规则

![image-20220915215331189](C:\Users\10244\AppData\Roaming\Typora\typora-user-images\image-20220915215331189.png)

#### 布尔类型Boolean的转换

布尔类型的转换是最简单的

它发生在逻辑运算中，但是也可以通过调用Boolean(value)显示地进行转换

转换规则如下

- 直观上为'空'的值(如0、空字符串、null、undefined、和NaN)将变成false
- 其他值变为true

## typeof操作符

**因为ECMAScript的类型系统是松散的，所以需要一种手段来确定任意变量的数据类型**

typeof操作符就是为此而生的

**对一个值使用typeof操作符会返回下列字符串之一**

- ‘undefined’表示值未定义
- ‘boolean’表示值未布尔值
- 'string'表示值为字符串
- 'number'表示值未数值
- 'object'表示值未对象或null
- 'function'表示值为函数
- 'symbol'表示值为符合

### typeof()用法

typeof(x) 与 typeof x 相同

typeof是一个操作符，**并非是一个函数**，()只是将后续的内容当做一个整体而已

## 运算

### 运算符

JavaScript按照使用场景的不同将运算符分成了很多种类型

算术运算符/赋值运算符/关系(比较)运算符/逻辑运算符

### 运算元

运算元--运算符应用的对象

如果一个运算符对应的只有一个运算元，那么它就是一元运算符

比如一元负号运算符  - 它的作用就是对数字进行正负转换

常见的一元运算符 + 和 - -号使用的会多一些

如果一个运算符拥有两个运算元，那么它就是二元运算符

比如2+3

### 算术运算符

算术运算符用在数学表达式中，它的使用方式和数学中是一致的

算术运算符是对数据进行计算的符号

![image-20220916202611690](C:\Users\10244\AppData\Roaming\Typora\typora-user-images\image-20220916202611690.png)

取余 % 和 求幂

a % b 的结果是a 除以 b 的余数

求幂运算 a **b 将a提升至a的b次幂

```js
console.log(2 ** 3) // 8
```

### 赋值运算符

 =  赋值运算符



原地修改

我们经常需要对一个变量做运算，并将新的结果存储在同一个变量中

```js
var n = 10
n = n+ 5
n = n * 2
```

可以使用运算符+=  和 *=来缩写这种表示

```js
var n = 10
    n +=5
    n *=2
```

![image-20220916203323995](C:\Users\10244\AppData\Roaming\Typora\typora-user-images\image-20220916203323995.png)

### 自增和自减

对一个数进行加一 、 减一是常见的数学运算符之一

所以，对此有一些专门的运算符

自增++ 将变量加1

自减 -- 将变量减1

自增自减只能应用于变量

将其应用于数值(比如5++)则会报错

#### ++ 和 -- 的位置

运算符 ++ 和 -- 可以置于变量前，也可以置于变量后

当运算符置于变量后，被称为“后置形式" :counter++

当运算符置于变量前，被称为“前置形式" :++counter

两者都做同一件事情，将变量counter加1

前置和后置的区别

只有当我们使用++ / --的返回值时才能看到区别

如果自增/自减的值不会被使用，那么两者形式没有区别

如果我们想要对变量进行自增操作，并且需要立刻使用自增后的值，那么我们需要使用前置形式

前置形式返回一个新的值，但后置返回原来的值

### 比较运算符

比较运算符的结果都是Boolean类型

#### === 和 == 的区别

普通的 == 存在一个问题，它不能区分 0 和 false 或者空字符串和false

这是因为在比较不同类型的值时，处于判断符号 == 两侧的值会先被转换为数字

空字符串 和false 也是如此，转化后它们都为数字0

严格运算符 === 就不会存在这种问题

=== 在进行比较时，不会做任何数据类型的转换

## 分支语句

### 程序的执行顺序

在程序开发中，程序有三种不同的执行方式

顺序 ---- 从上到下，顺序执行代码

分支 ----- 根据条件判断，决定执行代码的分支

循环 ----- 让特定代码 重复执行

![image-20220916205003799](C:\Users\10244\AppData\Roaming\Typora\typora-user-images\image-20220916205003799.png)

javas中常见的分支结构有

if分支结构

switch分支结构

### if分支语句

if分支结构有三种

单分支结构 if..

多分支结构

 if ..else ,,

 if ..else if..else,,

### 三元运算符

有时候我们需要根据一个条件去赋值一个变量

比如比较数字大小的时候，获取较大的数字，这个时候if else 语句就会显得过于臃肿吗，这个时候用三元运算符就比较简洁

条件运算符:'?'

? 被称为三元运算符，是因为该运算符中有三个操作数（运算元）

实际上它是JavaScript中唯一一个有这么多操作数的运算符

```javascript
const result  = condition ? value1 : value2
// 计算条件结果：如果结果为真，返回value1，否则返回value2
```

### 逻辑运算符

逻辑运算符主要有三个

|| 或 

&& 与

! 非

它可以将多个表达式或者值放在一起来获取到一个最终的结果



| 运算符 | 运算规则     | 范例            | 结果  |
| ------ | ------------ | --------------- | ----- |
| &&     | 与：同时为真 | false &&true    | false |
| \|\|   | 或：一个为真 | false \|\| true | true  |
| !      | 非：取反     | !false          | true  |

### switch语句

switch 语句是分支结构的一种语句

它是通过判断表达式的结果（或者变量）是否等于case语句的常量，来执行相应的分支体的

与if语句不同的是，switch语句只能做值的相等判断(使用全等运算符===)，而if语句可以做值的范围判断

#### switc语句

switch语句至少有一个case代码块盒一个可选的dafault代码块

```js
switch(变量){
  case 常量1
      //语句一
    break
  case 常量2
    //语句二
    break
    default:
    //语句三
}
```

case穿透问题

一条case语句结束后，会自动执行下一个case语句

这种现象被称之为case穿透

break关键字

通过在每个case的代码块后添加break关键字来解决这个问题

## 循环语句

循环是一种重复运行同一代码的方法

如果是对某一个列表进行循环操作，我们通常也称之为遍历(traversal)或迭代(iteration)

在JavaScript中支持三种循环方式

- while循环
- do...while循环
- for 循环

### while循环

while循环语法

- 当条件成立时，执行代码块
- 当条件不成立时，跳出代码块

![image-20220917153513446](C:\Users\10244\AppData\Roaming\Typora\typora-user-images\image-20220917153513446.png)

```js
while(循环条件){
  // 循环代码块
}
  //  打印0~99的数字
  var count = 0
  while (count < 100) {
     console.log(count)
     count++
  }
```

如果条件一直成立(为true)，那么会产生死循环

- 这个时候必须通过关闭页面来停止死循环
- 开发中一定要避免死循环的产生

### do..while循环

do..while循环和while循环非常像，二者经常可以江湖替代

但是do..while的特点是不管条件是否成立，do循环都会先执行一次

```js
do{
    // 循环代码块
} while(循环条件)
    
// 打印10次Hello World
var count = 0
do {
  console.log("Hello World")
  count++
 } while (count < 10)
```

![image-20220917153938569](C:\Users\10244\AppData\Roaming\Typora\typora-user-images\image-20220917153938569.png)

### for循环

```js
for(begin;condition;step){
    // 循环代码块
}
for(let i = 0; i < 3; i++){
    console.log(i)    
}
```



| 语句段         | 例子           | 执行过程                                      |
| -------------- | -------------- | --------------------------------------------- |
| begin          | let i = 0      | 进入循环时执行一次                            |
| condition      | i < 3          | 在每次循环迭代之前检查，如果为false，停止循环 |
| body（循环体） | console.log(i) | 条件为真时，重复运行                          |
| step           | i++            | 在每次循环体迭代后执行                        |

begin执行一次，然后进行迭代，每次检查condition后，执行body和step

### 循环控制

循环跳转（控制）

break：直接跳出循环，循环结束

 break 某一条件满足时，退出循环，不再执行后续重复的代码

continue：跳过本次循环次，执行下一次循环体

continue指令是break的"轻量版"

continue 某一条件满足时，不执行后续重复的代码

## 函数

### 什么是函数

函数其实就是某段代码的封装，这段代码帮助我们完成某一个功能

默认情况下JavaScript引擎或浏览器会给我们提供一些已经实现好的函数

我们也可以编写属于自己的函数

### 函数的使用步骤

函数的使用包含两个步骤

声明函数---封装独立的功能

调用函数---享受封装的成果

声明函数，在js中也可以称为定义函数

声明函数的过程是对某些功能的封装过程

调用函数，也可以称为函数调用

调用函数是让已存在的函数为我们所用

#### 函数的作用

在开发程序时，使用函数可以提高编写的效率及代码的重用

#### 声明和调用函数

声明函数使用function关键字，这种写法称之为函数的定义

函数定义完后里面的代码是不会执行的，函数必须调用才会执行

调用函数：通过函数名()即可，比如  test()

### 函数的参数

函数：把具有独立功能的代码块组织为一个小模块，在需要的时候调用

函数的参数：增加函数的通用性，针对相同的数据处理逻辑，能够适应更多的数据

  在函数内部，把参数当做变量使用，进行需要的数据处理

  函数调用时，按照函数定义的参数顺序，把希望在函数内部处理的数据，通过参数传递

#### 形参和实参

形参(参数 parameter)：定义函数时，小括号中的参数，是用来接收参数用的，在函数内部作为变量使用

实参(参数 argument)：调用函数时，小括号中的参数，是用来把数据传递到函数内部用的

#### arguments参数

函数有一个特别的对象：arguments对象

默认情况下，arguments对象是所有（非箭头）函数中都可用的局部变量

该对象中存放着所有的调用者传入的参数，从0位置开始，依次存放

arguments变量的类型是一个object类型（array-like），不是一个数组，但是和数组的用法看起来很相似

如果调用者传入的参数多余函数接收的参数，可以通过arguments去获取所有的参数

### 函数的返回值

函数不仅可以有参数，还可以有返回值

使用return关键字来返回结果

一旦在函数中执行return操作，那么当前函数会终止

如果函数中没有使用return语句，那么函数有默认的返回值：undefined

如果函数使用return语句，但是return后面没有任何值，那么函数的返回值也是undefined

### 函数中调用函数

函数内部是可以调用另一个函数的

```js
function foo(){
   console.log('foo被调用了')
}
function bar(){
  foo()
}
bar()
```

#### 函数的递归

函数调用自己，叫做递归

递归必须有结束条件，否则会产生无限调用，造成报错

```js
// 用递归实现一个自己的幂函数
function pow1(a,n){
    if(n===1) return a
    return a * pow(n-1)
}

// 用for循环实现一个自己的幂函数
function pow2(a,n){
    const result = 1
    for(var i = 0;i<n;i++){
        result *=a
    }
    return result
}
//用递归实现斐波拉契数
function febolaqi(n){
    if(n === 1 || n === 2) return 1
  retrun  febolaqi(n-2) + febolaqi(n-1)
    
}
//用for实现斐波拉契数
function fn(n){
    var n1 = 1
    var n2 = 1
    var result = 0
    if(n === 1 || n=== 2) return 1
    for(let i = 3;i <= n;i++){
        result = n1 + n2
        n1 = n2
        n2 = result  
    }
    return result
}
```

### 局部变量和外部变量

在js(ES5之前)中没有块级作用域，单数函数可以定义自己的作用域

作用域(scope)表示一些标识符的作用有效范围

函数的作用域表示在函数内部定义的变量，只有在函数内部可以被访问到

#### 外部变量和局部变量的概念

定义在函数内部的变量，被称之为局部变量

定义在函数外部的变量，被称之为外部变量

什么是全局变量

在函数之外声明的变量(在script中声明的)，称之为全局变量

全局变量在任何函数中都是可见的

通过var声明的全局变量会在window对象上添加一个属性

#### 在函数中，访问变量的顺序

优先反问自己函数中的变量，没有找到时，在外部中访问

### 函数表达式

在JavaScript中，函数并不是一种神奇的语法结构。而是一种特殊的值

前面定义函数的方式，我们称之为函数的声明

还有另外一种写法是函数表达式

```js
var foo = function(){  // 注意，function关键字后面没有函数名
    console.log('foo')  // 函数表示式允许省略函数名
}
```

#### 函数声明 vs 函数表达式

首先，语法不同

函数声明:在主代码流中声明为单独的语句的函数

函数表达式:在一个表达式中或另一个语法结构中创建的函数

其次，JavaScript创建函数的时机是不同的

函数表达式是在代码执行到达时被创建，并且仅从那一刻起可用

在函数声明被定义之前，它就可以被调用

这是内部算法的缘故

当js准备运行脚本的时候，首先会在脚本中寻找全局函数声明，并创建这些函数

### JavaScript头等函数

头等函数（first-class function；第一级函数）是指在程序设计语言中，函数被当作头等公民

这意味着，函数可以作为别的函数的参数、函数的返回值，赋值给变量或存储在数据结构中

通常我们对作为头等公民的编程方式，称之为函数式编程

js就是符合函数式编程的语言

比如函数可以在变量和变量直接相互赋值

```js
function foo(){
    console.log('foo')
}
var bar = foo
bar()
```

#### 回调函数

既然函数可以作为一个值相互赋值，那么也可以传递给另外一个函数

```js
function foo(fn){
    fn()
}
fuction bar(){
    console.log('bar')
}
foo(bar)
```

foo这种函数也称为高阶函数

#### 高阶函数

高阶函数必须至少满足以下两个条件之其中之一

- 接受一个或多个函数作为输入
- 输出一个函数

#### 匿名函数

如果在传入一个函数时，我们没有指定这个函数的名词或者通过函数表达式指定函数的对应的变量，那么这个函数称之为匿名函数

#### 立即执行函数

概念:Immediately-Invoked Function Expression（IIFE立即调用函数表达式）

一个函数定义完之后被立即执行

-   第一部分是定义了一个匿名函数，这个函数有自己独立作用域
-   第二部分是后面的()，表示这个函数被执行了

```js
(function(){
    console.log('立即执行函数')
})()
```

立即执行函数的应用

```js
var btns = document.querySelectorAll('.btn')
for(var i = 0; i < btns.length; i++) {
    (function(m){
        btns[m].onclick = function() {
            console.log(`第${m}个按钮被点击了`)
        }
    })(i)
}
```

