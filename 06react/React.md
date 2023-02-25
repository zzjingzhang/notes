# React

## React的开发依赖

### 开发React必须依赖三个库

- react:包含react所必须的核心代码
- react-dom:react渲染在不同平台所需要的核心代码
- babel:将jsx替换称React代码的工具

### 为什么要进行拆分呢？原因就是react-native

- react包中包含了react web 和 react-native所共同拥有的核心代码

- react-dom针对web和native所完成的事情不同

  web端:react-dom会将jsx最终渲染成真实的DOM，显示在浏览器中

  native端：react-dom会将jsx最终渲染成原生的控件(比如Andiord中的Button，IOS中的UIButton)

### babel是什么

- Babel，又名babel.js
- 是目前前端使用非常广泛的编译器，转移器
- 当下很多浏览器并不支持ES6语法，Babel工具可以将ES6转成大多数浏览器都支持的ES5语法

### React和Babel的关系

- 默认情况下**开发react其实可以不使用babel**
- 但是前提是我们**自己使用React.createElement来编写源代码**，它编写的代码**非常繁琐和可读性差**
- 我们可以直接编写**jsx(JavaScript Xml)**的语法，并且**让babel帮助我们转换成React.createElement**

##  组件化开发

整个逻辑可以看做一个整体，那么我们就可以将其封装成一个组件

root.render 的参数是一个HTML元素或者一个组件，所以我们可以像将之前的业务逻辑封装到一个组件中，然后传到ReactDOM.render 函数中的第一个参数

在react中，如何封装一个组件？这里暂时使用类的方式封装组件

1.定义一个类（类名大写，组件的名称是必须大写的，小写会被认为是html元素），继承自React.Component

2.实现当前组件的render函数

render当中返回的jsx内容，就是之后react会帮助我们渲染的内容

### 组件化-数据依赖

#### 组件化问题一：数据在哪里定义？

**在组件中的数据，我们可以分成两类**

1.参与界面更新的数据：当数据变量时，需要更新组件渲染的内容

2.不参与界面更新的数据：当数据变量时，不需要更新组件渲染的内容

**参与界面更新的数据我们也称之为是*参与数据流*，这个数据是<u>定义在当前对象的state</u>中**

我们可以通过构造函数中this.state = {定义数据}

当我们的数据发生变化时，我们可以调用this.setState 来更新数据，并且通知react进行update操作

在进行update操作时，就会重新调用render函数，并且使用最新的数据，来渲染界面

#### 组件化问题二：事件绑定中的this

在类中直接定义一个函数，并且将这个函数绑定到元素的onClick事件上，当前这个函数的this指向默认情况下是undefined

因为在正常的DOM操作中，监听点击，监听函数中的this其实是节点对象（比如说是button对象）

但是这次react并不是直接渲染成真实的DOM，我们所编写的button只是一个语法糖，它的本质React的Element对象

那么在这里发生监听的时候，react在执行函数时并没有绑定this，所以默认情况下是一个undefined

我们在

绑定的函数中，可能想要使用当前对象，比如执行this.setState函数，就必须拿到当前对象的this

我们需要在传入函数的时候。给这个函数直接绑定this

类似于下面的写法

```html
<button onClick={this.changeText.bind(this)}>改变文本</button>
```

