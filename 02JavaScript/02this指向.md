# this

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

以默认的方式调用一个函数，this指向widow

通过对象调用，this指向调用的对象

```js
function foo(){
    console.log(this)  // window
}
foo()

var obj = {
    bar:function(){
        console.log(this) // obj
    }
}
obj.bar()
```

