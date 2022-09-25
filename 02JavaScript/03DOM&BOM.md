# DOM & BOM

window全局对象

<img src="C:\Users\10244\Desktop\前端\notes\02JavaScript\images\06window全局对象.png" style="zoom:60%;" />

## DOM

DOM 文档对象模型(Document Object Model)

简称DOM，将页面所有的内容表示为可以修改的对象

### 理解DOM

**浏览器会对我们编写的HTML 、CSS进行渲染，同时它又要考虑我们可能会通过js来进行操作**

- 于是浏览器将我们编写的HTML中的每一个元素(element)都抽象成了一个个对象
- 所有这些对象都可以通过js来对其进行访问，那么我们就可以通过js来操作页面
- 所以，我们将这个抽象过程称之为文档对象模型（document object model）

**整个文档被抽象到document对象中**

- 比如document.documentElement对应的是html元素
- 比如document.body对应的是body元素
- 比如document.head对应的是head元素

### DOM Tree的理解

一个页面不只有html、head、body元素，也包括很多的子元素

在html结构中，最终会形成一个树结构

在抽象成DOM对象的时候，他们也会形成一个树结构，我们称之为DOM Tree

<img src="C:\Users\10244\Desktop\前端\notes\02JavaScript\images\07DOMTree.png" style="zoom:60%;" />

### DOM的继承关系图

**DOM相当于是js和html、css之间的桥梁**

通过浏览器提供给我们的DOM API，我们可以对元素以及其中的内容做任何事情

**类型之间有如下的继承关系**

<img src="C:\Users\10244\Desktop\前端\notes\02JavaScript\images\08DOM的继承关系图.png" style="zoom:60%;" />

### document对象

**document节点表示的整个载入的网页，它的实例是全局的document对象**

对DOM的所有操作都是从document对象开始的

它是DOM的入口点，可以从document开始取访问任何节点元素

**对于顶层的html、head、body元素，我们可以直接在document对象中获取到**

```js
html元素：<html> = document.documentElement
body元素：<body> = document.body
head元素：<head> = document.head
文档声明：<!DOCTYPE html> = document.doctype
```

### 节点之间的导航

如果我们获取到一个节点（Node)之后，可以根据这个节点去获取其他的节点，我们称之为节点之间的导航

#### 节点之间存在如下关系

- 父节点：parentNode
- 前兄弟节点：previousSibling
- 后兄弟节点：nextSibling
- 子节点：childNodes
- 第一个子节点：firstChild
- 第二个子节点：lastChild

<img src="C:\Users\10244\Desktop\前端\notes\02JavaScript\images\09节点之间的关系.png" style="zoom:67%;" />

### 元素之间的导航

如果我们获取到一个元素（element)之后，可以根据这个元素去获取其他的元素，我们称之为元素之间的导航

#### 元素之间存在如下的关系

- 父元素：parentElement
- 前兄弟元素：previousElementSibling
- 后兄弟元素：nextElementSibling
- 子元素：children
- 第一个子元素：firstElementChild
- 第二个子元素：lastElementChild

<img src="C:\Users\10244\Desktop\前端\notes\02JavaScript\images\10元素之间的关系.png" style="zoom:60%;" />

### 表格元素的导航

**table元素除了支持上面给出的那些导航之后，还支持如下这些属性**

- table.rows --- tr元素的集合
- table.caption/tHead/tFoot---引用元素caption、thead、tfoot
- table.tBodies---tbody元素的集合

**thead、tfoot、tbody元素提供了rows属性**

- tbody.rows--表格内部tr元素的集合

**tr**

- tr.cells ---在给定tr中的td 和 th 单元格的集合
- tr.sectionRowIndex---给定的tr在封闭的thead/tbody/tfoot中的位置（索引）
- tr.rowIndex --- 在整个表格中tr的编号（包括表格的所有行）

**td 和 th**

- td.cellIndex--在封闭的tr中单元格的编号

### 获取元素的方法

| 方法名                | 搜索方式     | 是否可以在元素上调用 | 是否实时 |
| --------------------- | ------------ | -------------------- | -------- |
| querySelector         | CSS-selector | 是                   | 否       |
| querySelectorAll      | CSS-selector | 是                   | 否       |
| getElementById        | id           | 否                   | 否       |
| getElementByName      | name         | 否                   | 是       |
| getElementByTagName   | tag or *     | 是                   | 是       |
| getElementByClassName | class        | 是                   | 是       |

### 节点的属性(主要是共有属性)

nodeType：获取节点类型，是一个数值类型

nodeName：获取node节点的名称，是为任意node定义的

tagName：获取元素的标签名词  ，仅适用于element节点

innerHTML：将元素中的HTML获取为字符串形式，设置元素中的内容

textContent：仅仅获取元素中的文本内容

nodeValue(data)：用于获取非元素节点的文本内容

hidden：可以用于设置元素隐藏

### 元素的属性和特性

浏览器在解析HTML元素时，会将对应的attribute也创建出来放到对应的元素对象上

比如id、class就是全局的attribute，会有对应的id class属性

比如href属性是针对a元素的，type、value属性是针对input元素的

#### attribute的分类

标准的attribute：某些attribute属性是标准的，比如id、class、href、type、value等

非标准的attribute：某些attribute属性是自定义的，比如abc、age、height

```html
<div class="box" id="main" name="ke" abc="abc" age="18" heigth="1.88"></div>
```

#### attribute的操作

对于所有的attitude访问都支持如下的方法

elem.hasAttribute(name)：--检查特性是否存在

elem.getAttribute(name)：---获取这个特性值

elem.setAttribute(name，value)：--设置这个特性值

elem.removeAttribute(name)：--移出这个特性

attributes：attr对象的集合，具有name、value属性

#### attribute具备以下特征

- 他们的名字是大小写不敏感的（id与ID相同）
- 它们的值总是字符串类型的

### 元素的属性（property）

对于标准的attribute，会在DOM对象上创建与其对应的property属性

```js
console.log(boxEl.id,boxEl.className) // main box
console.log(boxEl.abc,boxEl.age) // undefined...
```

### HTML5的data-*自定义属性

自定义属性可以在dataset属性中获取到

```js
<div class="box" data-name="ke"  data-age="18"></div>
var boxEl = document.querySelector('.box')
console.log(boxEl.dataset.name) // ke
console.log(boxEl.dataset.age)  // 18
```

### 元素的className 和classList

元素的class attribute，对应的property并非叫class，而是className

这是因为js早期不允许使用class这种关键字来作为对象的属性，所以DOM规范使用了className

我们可以对className进行赋值，它会替换整个类中的字符串

如果我们需要添加或者移出单个class，可以使用classList属性

elem.classList是一个特殊的对象

```js
elem.classList.add(class):添加一个类
elem.classList.remove(class):移除一个类
elem.classList.toggle(class):如果类不存在就添加类，存在就移出它
elem.classList.contains(class):检查给定类，返回true/false
```

**classList是可迭代对象，可以通过for of遍历**

### 元素的style属性

如果需要单独修改某一个CSS属性，那么可以通过style来操作

对于多次属性，使用驼峰式 camelCase

```js
boxEl.style.width = '100px'
boxEl.style.backgroundColor="red"
```

如果我们将值设置为空字符串，那么会使用css的默认样式

```js
boxEl.style.display = '' // display 为默认值
```

#### 元素style的读取-getComputedStyle

如果我们需要读取样式

对于内联样式，是可以通过style.*读取到的

对于style、css文件中的样式，是读取不到的



这个时候可以通过getComputedStyle的全局函数来实现

```js
getComputedStyle(boxEl).width
```

### 创建元素

```js
document.createElement('h2')
```

### 插入元素

插入元素的方法如下

```js
node.append(...nodes or strings)---在node末尾插入节点或字符串
node.prepend(...nodes or strings)---在node开头插入节点或字符串
node.before(...nodes or strings)---在node前面插入节点或字符串
node.after(...nodes or strings)---在node后面插入节点或字符串
node.replaceWith(...nodes or strings)---将node替换为给定节点或字符串
```

<img src="C:\Users\10244\Desktop\前端\notes\02JavaScript\images\11插入元素.png" style="zoom:60%;" />

### 移除和克隆元素

移出元素我们可以调用元素本身的remove方法

```js
boxEl.remove()
```

如果我们想要复制一个现有的元素，可以通过cloneNode方法

可以传入一个Boolean类型的值，来决定是否深度克隆

深度克隆会克隆对应的元素的子元素。否则不会

```js
var cloneBoxEl = boxEl.cloneNode(true)
```

### 元素的大小、滚动

<img src="C:\Users\10244\Desktop\前端\notes\02JavaScript\images\12元素的大小、滚动.png" style="zoom:60%;" />

### window的大小、滚动

window的width和height

innerWidth、innerHeight：获取window窗口的宽度和高度（包含滚动条）

outerWidth、outerHeight：获取window窗口的整个宽度和高度（包括调试工具、工具栏）

documentElement.clientHeight、documentElement.clientWidth：获取html的宽度和高度（不包含滚动条）



window的滚动位置

scrollX：x轴滚动的位置（别名pageXOffset）

scrollY：Y轴滚动的位置（别名pageYOffset）



对应的滚动方法

scrollBy(x,y):将页面滚动至 相对于当前位置的（x，y）位置

scrollTo(pageX,pageY):将页面滚动至 绝对坐标

### 事件处理

#### 事件监听的方式

- 在script中直接监听（很少使用）
- DOM属性，通过元素on来监听事件
- 通过eventTarget中的addEventListener来监听

```js
<div id="box" onclick="alert('box点击')"></div>
box.onclick = function(){
    alert('box点击2')
}
box.addEventListener('click',fuction(){
   alert('box点击3')
})
```

#### 常见的事件列表

##### 鼠标事件

click ---- 当鼠标点击一个元素时（触摸屏设备会在点击时生成）

mouseover/mouseout---- 当鼠标指针移入/离开一个元素时

mousedown/mouseup ---- 当在元素上按下/释放鼠标按钮时

mousemove---- 当鼠标移动时

##### 键盘事件

keydown 和 keyup --- 当按下和松开一个按键时

##### 表单（form）元素事件

submit --- 当访问者提交了一个form时

focus --- 当访问者聚焦于一个元素时，例如聚焦于一个input

##### document事件

DOMContentLoaded --- 当HTML的加载和处理均完成，DOM被完全构建完成时

##### css事件

transitioned --- 当一个css动画完成时

#### 事件冒泡和事件捕获

默认情况下事件是从最内层的元素向外依次传递的顺序，这个顺序我们称之为事件冒泡（Event Bubble）

**另外一种监听事件流的从外层到内层的方式，称之为事件捕获（Event Capture）**

**为什么会产生两种不同的处理流呢**

- 这是因为早期浏览器开发时，不管是IE还是Netscape公司都发现了这个问题（对着元素点击时，点击的不仅仅是这个元素本身）
- 但是他们采用了完全相反的事件流来对事件进行了传递
- IE采用了事件冒泡的方式，Netscape采用了事件捕获的方式

<img src="C:\Users\10244\Desktop\前端\notes\02JavaScript\images\13事件冒泡和事件捕获.png" style="zoom:60%;" />

#### 事件捕获和冒泡的过程

如果我们同时监听冒泡和捕获，那么会按照如下顺序来执行

捕获阶段

事件从window向下走近元素

目标阶段

事件到达目标元素

冒泡阶段

事件从元素上开始冒泡

事实上，我们可以通过event对象来获取当期的阶段

eventPhase

<img src="C:\Users\10244\Desktop\前端\notes\02JavaScript\images\14事件冒泡和捕获的过程.png" style="zoom:60%;" />

#### 事件对象

当一个事件发生时，就会有和这个事件相关的很多信息

- 比如事件的类型是什么，你点击的是哪一个元素，点击的位置是哪里等等相关信息
- 这些信息会被封装到一个event对象中，这个对象由浏览器创建，称之为event对象
- 该对象给我们提供了想要的一些属性，以及可以通过该对象进行某些操作

##### 获取event对象

event对象会在传入的事件处理函数回调时，被系统传入

我们可以在这个回调函数中拿到这个event对象

```js
spanEl.onclick = function(event){
    console.log(event,'事件对象')
}
spanEl.addEventListener('click',functions(event){
   console.log(event,'事件对象')
 })
```

##### event中常见的属性和方法

###### 常见的属性

```js
type:事件的类型
target:当前事件发生的元素
currentTarget:当前处理事件的元素
eventPhase:事件所处的阶段
offsetX offsetY:事件发生在元素内的位置
clientX clientY:事件发生在客户端内的位置
pageX pageY:事件发生在客户端相对于document的位置
screenX screeY:事件发生相对于屏幕的位置
```

###### 常见的方法

```js
preventDefault:取消事件的默认行为
stopPropagation:阻止事件的进一步传递（冒泡或者捕获都可以阻止）
```

#### EventTarget类

所有的节点、元素都继承自EventTarget

事实上window也继承自EventTarget

EventTarget 是一个DOM接口。主要用于添加、删除、派发event事件

##### EventTarget常见的方法

```js
addEventListener:注册某个事件类型以及事件处理函数
removeEventListener:移除某个事件类型以及事件处理函数
dispatchEvent:派发某个事件类型到eventTarget上
```

```js
var boxEl = document.querySelector('.box')
boxEl.addEventListener('click',function(){
    console.log('box')
})

//派发event事件
boxEl.addEventListener('click',function(){
    window.dispatchEvent(new Event('abc'))
})

boxEl.addEventListener('abc',function(event){
    console.log('监听abc事件',event)
})
```

#### 事件委托

事件冒泡在某种情况下可以帮助我们实现强大的事件处理模式-事件委托模式（也是一种设计模式）

当子元素被点击时，父元素可以通过冒泡监听到子元素的点击，并且可以通过event.target获取到当前监听的元素

案例：在一个ul中存放多个li，点击某一个li会变成红色

方案一：监听每一个li，并且做出相应的改变

方案二：在lu中监听点击，并且通过event.target拿到对应的li进行处理

方案二并不需要遍历后给每个li上添加事件监听，所以更加高效

#### 常见的鼠标事件

常见的鼠标事件（不仅仅是鼠标设备，也包括模拟鼠标的设备，比如手机，平板电脑等）

| 属性        | 描述                                           |
| ----------- | ---------------------------------------------- |
| click       | 当用户点击某个对象时调用的事件句柄             |
| contextmenu | 在用户点击鼠标右键打开上下文菜单时触发         |
| dbclick     | 当用户双击某个对象时调用的事件句柄             |
| mousedown   | 鼠标按钮被安息                                 |
| mouseup     | 鼠标按钮被松开                                 |
| mouseover   | 鼠标移动到某个元素之上（支持冒泡）             |
| mouseout    | 鼠标从某元素移开（支持冒泡）                   |
| mouseenter  | 当鼠标指针移动到某个元素上时触发（不支持冒泡） |
| mouseleave  | 当鼠标指针移出元素上时触发（不支持冒泡）       |
| mousemove   | 鼠标被移动                                     |

#### 常见的键盘事件

| 属性       | 描述               |
| ---------- | ------------------ |
| onkeydown  | 某个键盘按键被按下 |
| onkeypress | 某个键盘按键被按下 |
| onkeyup    | 某个键盘按键被松开 |

事件的执行顺序是onkeydown 、onkeypress 、onkeyup

down事件先发生

press发生在文本被输入

up发生在文本输入完成

我们可以通过key 和 code 来区分按下的键

code：“按键代码”（如“KeyA",”ArrowLeft“等），特定于键盘上按钮的物理位置

key：字符（"A",“a“等），对于非字符的按键，通常具有与code相同的值

#### 常见的表单事件

| 属性     | 描述                                                         |
| -------- | ------------------------------------------------------------ |
| onchange | 该事件在表单元素的内容改变时触发（input、keygen、select、textarea） |
| oninput  | 元素获取用户输入时触发                                       |
| onfocus  | 元素获取焦点时触发                                           |
| onblur   | 元素失去焦点时触发                                           |
| onreset  | 表单重置时触发                                               |
| onsubmit | 表单提交时触发                                               |

#### 文档加载事件

DOMContentLoaded ：浏览器已完全加载html，并构建了DOM树，但像img和样式表之类的外部资源可能尚未加载完成

load：浏览器不仅加载完成了html，还加载完成了所有外部资源：图片，样式等

## BOM

BOM 浏览器对象模型(Browser Object Model)

简称BOM，由浏览器提供的用于处理文档(document)之外的所有内容的其他对象

比如navigatior、location、history等对象

js有一个非常重要的运行环境就是浏览器

而且浏览器本身又作为一个应用程序需要对其进行操作

所以通常浏览器会有 对应的对象的模型

我们可以将BOM看成是连接js脚本与浏览器窗口的桥梁

BOM主要包括以下的对象模型

window：包括全局属性、方法，控制浏览器窗口相关的属性、方法

location：浏览器连接到的对象的位置（url）

history：操作浏览器的历史

navigator：用户代理（浏览器）的状态和标识（很少用到）

screen：屏幕窗口信息（很少用到）

### window对象

window对象在浏览器中可以从两个视角来看待

视角一：全局对象

ECMAScript有一个全局对象，这个全局对象在Node中global，在浏览器中就是window对象

视角二

作为浏览器窗口时，提供了对浏览器操作的相关api

放在window对象上的所有属性都可以被访问

使用var定义的变量会被添加到window对象中

window默认给我们提供了全局的函数和类：setTimeout、Math、Date、Object等

#### window对象的作用

事实上window对象上肩负的重担是非常大的

第一：包含大量的属性，localStorage、console、location、history、screeX、scrollX等等（大概60+个属性）

第二：包含大量的方法，alert，close、scrollTo、open等（大概40+个方法）

第三：包含大量的事件，focus、blur、load、hashchange等（大概30+个事件）

第四：包含从EventTarget继承过来的方法，addEventListener，removeEventListener，dispatchEvent方法

```
MDN文档https://developer.mozilla.org/zh-CN/docs/Web/API/Window
```

#### window常见的属性

```js
// 浏览器高度
window.outerHeight
window.innerHeight

window.screenX
window.screenY

// 监听
window.addEventListener('scroll',(event)=>{
    console.log(window.scrollX)
     console.log(window.scrollY)
})
```

#### window常见的方法

```js
// close 方法
const closeBtn = document.querySelector('#close')
closeBtn.onclick = function(){
    close()
}

// scrollTo
const scrollBtn = document.querySelector('#scroll')
scrollBtn.onclick = function(){
    scrollTo({top:1000})
}

// 打开新创建
const openBtn = document.querySelector('#open')
openBtn.onclick = function(){
    open('url','_self')
}
```

#### window常见的事件

```js
window.onfocus = function(){
    console.log('窗口获取到焦点')
}

window.onblur = function(){
    console.log('窗口失去了焦点')
}

// 整个页面以及所有的资源都加载完成
window.onload = function(){
    console.log('页面加载完成')
}

// hash 改变
const hashBtn = document.querySelector('#hash')
hashBtn.onclick = function(){
   location.hash = 'aaa'
}
window.onhashchange = function(){
     console.log('hash被修改了')
}
```

#### location对象

location对象用于表示window上当前链接到的URL信息

##### location对象常见的属性

href:当前window对应的超链接URL，整个URL

protocol：当前的协议

host：主机地址

hostname：主机地址（不带端口）

port：端口

pathname：路径

search：查询字符串

hash：哈希值

##### location对象常见的方法

assign：赋值一个新的URL，并且跳转到该URL中

replace：打开一个新的URL，并且跳转到该URL中（不同的是不会在浏览记录中留下之前的记录）

reload：重新加载页面，可以传入一个Boolean类型

#### URLSearchParams

URLSearchParams 定义了一些实用的方法来处理URL查询字符串

可以将一个字符串转换成URLSearchParams类型

也可以将URLSearchParams类型转换成字符串

```js
var urlsearch = new URLSearchParams("name=abc&age=18&height=1.88")
console.log(urlsearch.get('name')) // abc
console.log(urlsearch.toString()) // name=abc&age=18&height=1.88
```

##### URLSearchParams常见的方法

get：获取搜索参数的值

set：设置一个搜索参数和值

append：追加一个搜索参数和值

has：判断是否有某个搜索参数值

```js
mdn文档地址  https://developer.mozilla.org/zh-CN/docs/Web/API/URLSearchParams
```

中文会使用 encodeURIComponent  和 decodeURIComponent 进行编码和解码

#### history对象常见的属性和方法

history 对象允许我们访问浏览器曾经的会话历史记录

##### 有两个属性

length：会话中的记录条数

state：当前保留的状态值

##### 有五个方法

back()：返回上一页，等价于history.go(-1)

forward()：前进下一页，等价于history.go(1)

go()：加载历史中的某一页

pushState()：打开一个指定的地址

replaceState()：打开一个新的地址，并且使用replace

```js
history.length
history.state

const jumpBtn = document.querySelector('#jump')
const backBtn = document.querySelector('#back')
jumpBtn.onclick = function(){
    history.pushState({name:'abc'},'11','aa')
    console.log(history.length,history.state)
}

backBtn.onclick = function(){
    history.back()
    console.log(history.length,history.state)
}
```

#### navigator对象（很少使用）

navigator对象表示用户代理的状态和标识等信息

#### screen对象（很少使用）

screen主要记录的是浏览器窗口外面的客户端显示器的信息

比如屏幕的逻辑像素 screen.width 、screen.height

### JSON

在目前的开发中，json是一种非常重要的数据格式，它并不是编程语言，而是一种可以在服务器和客户端之间传输的数据格式

json全称： JavaScript Object Notation （JavaScript对象符号）



#### JSON 的基本语法

JSON的顶层支持三种类型的值

简单值：数字（number）、字符串（string，不支持单引号）、布尔类型（Boolean）、null类型

对象值：由key、value组成，key是字符串类型，并且必须添加双引号，值可以是简单值，对象值。数组值

数组值：数组值可以是简单值，对象值。数组值

#### JSON序列化

stringify方法：将js类型转换成对应的json字符串（序列化）

parse方法：解析json字符串，转回对应的js类型（反序列化）

```js
const objString = JSON.stringify(obj)
localStorage.setItem('info',objString)

const itemString = localStorage.getItem('info')
const info = JSON.parse(itemString)
```

##### stringify的参数replace

 JSON.stringify()方法将一个js对象或值转换为JSON字符串

如果指定了一个replace函数，则可以选择性地替换值

如果指定的replace是数组，则可以选择性地仅包含数组指定的属性

```js
 const obj = {
      name: "why",
      age: 18,
      friend: {
        name: "kobe"
      },
     hobbies:["篮球","足球"]
    }

// 转成字符串
const objString = JSON.stringify(obj)
// {"name":"why","age":"18","friend":{"name":"kobe"},"hobbies":["篮球","足球"]}

// replace参数是一个数组
const objString2 = JSON.stringify(obj,["name","age"])
// {"name":"why","age":18}


//replace参数是一个函数
const objString3 = JSON.stringify(obj,(key,value)=>{
    if(key === 'name'){
        return "abc"
    }
    return value
}) // {"name":"abc","age":"18","friend":{"name":"abc"},"hobbies":["篮球","足球"]}

```

##### stringify的参数space

如果对象本身包含toJSON方法，那么会直接使用toJSON方法的结果

```js
 const obj = {
      name: "why",
      age: 18,
      friend: {
        name: "kobe"
      },
     hobbies:["篮球","足球"],
     toJSON:function(){
         return 'abc'
     }
    }
 const obj1 = JSON.stringify(obj) // abc
```

### 认识Storage

webStorage主要提供了一种机制，可以让浏览器提供一种比cookie更直观的key、value存储方式

localStorage：本地存储，提供的是一种永久性的存储方法，在关闭掉网页重新打开时，存储的内容依然保留

sessionStorage：会话存储，提供的是本次会话的存储，在关闭掉会话时，存储的内容会被清除

##### localStorage 和 sessionStorage的区别

验证一：关闭网页后重新打开，localStorage 会保留，而sessionStorage会被删除

验证二：在页面内实现跳转localStorage 会保留，sessionStorage也会被保留

验证三：在页面外实现跳转（打开新的网页），localStorage 会保留，sessionStorage不会被保留

##### Storage常见的属性和方法

###### 属性

Storage.length：只读属性

 返回一个整数，表示存储在storage对象中的数据项数量

###### 方法

Storage.key()：该方法接受一个数值n作为参数，返回存储中的第n个key名称

Storage.getItem()：该方法接受一个key作为参数，并且返回key对应的value

Storage.setItem()：该方法接受一个key和value作为参数，并且将会把key和value添加到存储中，如果key存储，则更新其对应的值

Storage.removeItem()：该方法接受一个key作为参数，并把该key从存储中删除

Storage.clear()：该方法的作用是清空存储中的所有key