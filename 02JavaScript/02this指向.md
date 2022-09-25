# this

**这里this绑定显示的值均指在非严格模式下的值**

## 为什么需要this

在常见的编程语言中，几乎都有this这个关键字(Objective-C中使用的是self)，但是js中的this和常见的面向对象语言中的this不太一样

- 常见的面向对象的编程语言中，比如Java、C++、Swif、Dart等一系列语言中，this通常只会出现在类的方法中
- 也就是你需要一个类，类中的方法（特别是实例方法）中，this代表的是当前调用对象

**但是js中的this更加灵活，无论是它出现的位置还是它代表的含义**

如下代码，有this 和没有this的区别

```js
var obj = {
    name:'kb',
    running:function(){
        console.log(obj.name + 'running')
    },
    eating:function(){
        console.log(obj.name + 'eating')
    }
}

var obj2 = {
    name:'kb',
    running:function(){
        console.log(this.name + 'running')
    },
    eating:function(){
        console.log(this.name + 'eating')
    }
}
```

## this指向什么

```js
// 定义一个函数
function foo(){
    console.log(this)
}
// 1.调用方式一：直接调用
foo() // window
// 2.调用方式二：将foo放到一个对象中，再调用
var obj = {
    name:'abc',
    foo:foo
}
obj.foo() // obj对象

// 3调用方式三:通过call/apply调用
foo.call('abc') // String {"abc"}对象
```

上面的案例给我们的启示

- 函数在调用时，js会默认给this绑定一个值
- this的绑定和定义的位置（编写的位置）没有关系
- this的绑定和调用方式以及调用的位置有关系
- this是在运行时被绑定的

## this绑定规则

- 默认绑定
- 隐式绑定
- 显式绑定
- new 绑定

### 默认绑定

什么情况下使用默认绑定呢？独立函数调用

独立函数的调用我们可以理解成函数没有被绑定到某个对象上进行调用

常见的默认绑定

```js
// 1
function foo(){
    console.log(this)
}
foo(); // window

//2 
function test1(){
    console.log(this)
    test2()
};

function test2(){
    console.log(this)
    test3()
};

function test3(){
    console.log(this)
};
test1();

// 3
function foo(func){
    func()
}
var obj = {
    name:'why',
    bar:function(){
        console.log(this)
    }
}

foo(obj.bar)
```

### 隐式绑定

通过某个对象进行调用的

也就是它的调用位置中，是通过某个对象发起的函数调用

常见的隐式调用

```js
// 1
function foo(){
    console.log(this)  // obj对象
};
var obj ={
    name:"why",
    foo:foo
};
obj.foo();

// 2
function foo(){
    console.log(this)  // obj2对象
}
var obj1 = {
    name:'obj1',
    foo:foo
}
var obj2 = {
    name:"obj2",
    obj1:obj1
}
obj2.obj1.foo()
```

### 显式绑定

隐式绑定有一个前提条件

必须在调用的对象内部有一个函数的引用（比如一个属性）

如果没有这样的引用，在进行调用的时候，会报找不到该函数的错误

正是通过这个引用，间接的将this绑定到了这个对象上

如果我们不希望在对象内部包含这个函数的引用，同时又希望在这个对象上进行强调引用，该怎么做呢？

js的所有函数都可以使用**call/apply**方法

call 和 apply  

第一个参数是相同的，要求传入一个对象

这个对象的作用就是给this准备的，在调用这个函数的时候，会将this绑定到这个传入的对象上

后面的参数，apply为数组，call为参数列表

```js
func.apply(thisArg,[argsArray])
func.call(thisArg,arg1,arg2,...)
          
```

#### **通过call或apply绑定this对象**

显式绑定后，this就会明确指向绑定的对象

```js

var obj = {
    name:'obj'
}
function foo(){
    console.log(this)
}
foo.call(obj) // this->obj对象
foo.apply(obj) // this->obj对象
```

因为这个过程，我们明确的绑定了this指向的对象，所以称之为显式绑定

#### 通过bind绑定this对象

如果我们希望一个函数总是显式的绑定到一个对象上，可以怎么做呢？

使用bind方法，bind()方法创建一个新的绑定函数（bound function ，BF)

绑定函数是一个exotic function object （怪异函数对象，ECMAScript2015种的术语）

在bind()被调用时，这个新函数的this被指定为bind()的第一个参数，而其余参数将作为新的函数的参数，供调用时使用

```js
function.bind(thisArg[,arg1[,arg2[,...]]])
```

```js
function foo(){
    console.log(this)
}

var obj = {
    name:'obj'
}
// 需求，调用foo时，总是绑定到obj对象身上（不希望obj对象身上有函数）
var baz = foo.bind(obj)
baz() // this指向obj对象
```

### new 绑定

js中的函数可以当做一个类的构造函数来使用，也就是new关键字

使用new关键字来调用函数时，会执行如下操作

1. 创建一个全新的对象
2. 这个新对象会被执行prototype连接
3. 这个新对象会绑定到函数调用的this上（this的绑定在这个步骤完成）
4. 执行函数体中代码块
5. 如果函数没有返回其他对象，表达式会返回这个新对象

```js
// 创建person
function Person(name){
    console.log(this) // Person {}
    this.name = name
}

var p = new Person('person1')
console.log(p) //Person {name: 'person1'}
```

### 规则优先级

- 默认规则的优先级最低
- 显示绑定优先级高于隐式绑定
- new绑定优先级高于隐式绑定
- new绑定优先级高于bind

​           new绑定和call、apply是不允许同时使用的，所以不存在谁的优先级更高

​           new绑定可以和bind一起使用，new绑定优先级更高

```js
 // function foo() {
    //   console.log("foo:", this)
    // }

    // 比较优先级:

    // 1.显式绑定绑定的优先级高于隐式绑定
    // 1.1.测试一:apply高于默认绑定
    // var obj = { foo: foo }
    // obj.foo.apply("abc")
    // obj.foo.call("abc")

    // 1.2.测试二:bind高于默认绑定
    // var bar = foo.bind("aaa")
    // var obj = {
    //   name: "why",
    //   baz: bar
    // }
    // obj.baz()


    // 2.new绑定优先级高于隐式绑定
    // var obj = {
    //   name: "why",
    //   foo: function() {
    //     console.log("foo:", this)
    //     console.log("foo:", this === obj)
    //   }
    // }
    // new obj.foo()


    // 3.new/显式
    // 3.1. new不可以和apply/call一起使用

    // 3.2. new优先级高于bind
    // function foo() {
    //   console.log("foo:", this)
    // }
    // var bindFn = foo.bind("aaa")
    // new bindFn()


    // 4.bind/apply优先级
    // bind优先级高于apply/call
    function foo() {
      console.log("foo:", this)
    }
    var bindFn = foo.bind("aaa")
    bindFn.call("bbb")

```

### this规则之外-忽略显示绑定

情况一：如果在显示绑定中，我吗传入一个null或undefined，那么这个显示绑定会被忽略，使用默认规则

```js
function foo(){
  console.log(this)
}
var obj = {
   name:'obj'
}
foo.call(obj) // obj对象
foo.call(null) // window
foo.call(undefined)// window

var bar = foo.bind(null)
bar() // window
```

### this规则之外-间接函数引用

情况二，创建一个函数的间接引用，这种情况使用默认绑定规则

```js
function  foo(){
    console.log(this)
}

var obj1 = {
    name:'obj1',
    foo:foo
}

var obj2 = {
    name:'obj2'
}

obj1.foo() // obj1对象
(obj2.foo = obj1.foo)() // window
```

## 箭头函数

箭头函数是ES6之后增加的一种编写函数的方法，并且它比函数表达式更加简洁

- 箭头函数不会绑定this、arguments属性
- 箭头函数不能作为构造函数来使用（不能和new一起来使用，会抛出错误）

语法

():函数参数

{}:函数的执行体

```js
nums.forEach((item,index,arr)=>{
    
})
```

### 箭头函数的编写优化

```js
// 1如果只有一个参数 () 可以省略
nums.forEach(item=>{})

// 2.如果函数执行体中只有一行代码，那么可以省略大括号
// 并且这行代码的返回值会作为整个函数的返回值
nums.forEach(item=>console.log(item))
nums.filter(item=>true)

// 3.如果函数执行体只有返回一个对象，那么需要给这个对象加上()
var foo = () =>{
    return {name:'abc'}
}
var bar = () => ({name:"abc"})
```

### this规则之外-es6箭头函数

箭头函数不能使用this的四种标准规则（也就是不绑定this），而是根据外层作用域来决定this

```js
    // 2.箭头函数中, 压根没有this
    var bar = () => {
      console.log("bar:", this)
     }
     bar()
  // 通过apply调用时, 也是没有this
    bar.apply("aaaa")
// 两个this均指向window
```

### 箭头函数中的this

箭头函数并不绑定this，那么this引用就会从上层作用域中找到对应的this