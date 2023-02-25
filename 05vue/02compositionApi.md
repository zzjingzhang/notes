## Composition `API`

### setup函数

setup函数主要有两个参数

第一个参数：props

第二个参数：context

#### props

就是父组件传递过来的属性会被放到props对象中，我们在setup中如果需要使用，那么就可以直接通过props参数获取

对于props的类型，和之前的规则一样，在props选项中定义

并且在template依然可以正常去使用props中的属性

如果我们在setup函数中想要使用props，那么不可以通过this去获取

因为props有直接作为参数传递到setup函数中，所以我们可以直接通过参数来使用即可

#### context

我们也称之为`SetupContext`，它里面包含三个属性

`attrs`：所有的非prop的attribute

slots：父组件传递过来的插槽（这个在以渲染函数返回时会有作用）

emit：当我们组件内部需要发出事件时会用到emit（因为不能访问this,所以不可以通过this.$emit发出事件）

#### setup函数的返回值

setup的返回值可以在模板template中被使用，也就是说我们可以通过setup的返回值来替代data选项

#### Reactive `API`

想为在setup中定义的数据提供响应式的特性，我们可以使用reactive的函数

```js
const state = reactive({
    name:'abc',
    counter:10
})
```

当我们使用reactive函数处理数据之后，数据再次被使用时会进行依赖收集

当数据发生改变时，所有收集到的依赖都是进行对应的响应式操作（比如更新界面）

#### Ref `API`

Reactive `API`对传入的类型是有限制的，它要求我们必须传入一个对象或者数组类型

如果我们传入一个基本数据类型(String,Number,Boolean)会报一个警告

这个时候`vue3`提供了另外一个`API:ref API`

ref会返回一个可变的响应式对象，该对象作为一个响应式的引用维护着它内部的值

它内部的值是在ref的value属性中被维护的

```js
const message = ref('hello world')
console.log(message.value)
```

注意：

1.在模板中引入ref的值时，`vue`会自动进行解包，所以我们并不需要在模板中通过`ref.value`的方式来使用

2.但是在setup函数内部，它依然是一个ref引用，所以对其进行操作时，需要使用`ref.value`的方式

模板中的解包是浅层解包

#### `readonly`

我们通过reactive或ref可以获取到一个响应式的对象，但是某些情况下，我们传入给其他地方（组件）的这个响应式对象希望在另外一个地方（组件）被使用，但是不能被修改，这个时候可以使用`readonly`方法

`readonly`会返回原始对象的只读代码（也就是它依然是一个proxy，这是一个proxy的set方法被劫持，并且不能对其进行修改）

在开发中常见的`readonly`方法会传入三个类型的参数

1.普通对象

2.`reactive`返回的对象

3.`ref`对象

##### `readonly`的使用

在`readonly`的使用过程中，有如下规则

`readonly`返回的对象都是不允许修改的

但是经过`readonly`处理的原来的对象是允许被修改的

比如`const` info = `readonly`(obj)，info对象是不允许被修改的，当obj被修改时，`readonly`返回的info对象也会被修改，但是我们不能去修改`readonly`返回的info对象

```js
// 传入普通对象
const info1 = {
    name:'abc',
    age:18
}
// 传入reactive对象 
const info2 = reactive({
      name: 'abc',
      age: 18,
      height: 1.88,
    })
// 传入ref对象
const nameRef = ref('abc')
```

其实本质上就是`readonly`返回的对象的setter方法被劫持了

`readonly` 的应用

在我们传递给其他组件数据时，往往希望其他组件使用我们传递的内容，但是不允许它们修改时，就可以使用`readonly`了；

#### reactive判断的`API`

##### **`isProxy`**

检查对象是否是由 reactive 或 `readonly`创建的 proxy。

##### `isReactive`

检查对象是否是由 reactive创建的响应式代理：

如果该代理是 `readonly` 建的，但包裹了由 reactive 创建的另一个代理，它也会返回 true；

##### `isReadonly`

检查对象是否是由 `readonly` 创建的只读代理。

#####  `toRaw`

返回 reactive 或 `readonly` 代理的原始对象（**不**建议保留对原始对象的持久引用。请谨慎使用）。

##### `shallowReactive`

创建一个响应式代理，它跟踪其自身 property 的响应性，但不执行嵌套对象的深层响应式转换 (深层还是原生对象)。

##### `shallowReadonly`

创建一个 proxy，使其自身的 property 为只读，但不执行嵌套对象的深度只读转换（深层还是可读、可写的）。

#### `toRefs`

如果我们使用`ES6`的解构语法，对reactive返回的对象进行解构获取值，那么之后无论是修改结构后的变量，还是修改reactive

返回的info对象，数据都不再是响应式的：

```js
const info = reactive({
  name: 'abc',
  age: 18,
  height: 1.88,
})
```

那么有没有办法让我们解构出来的属性是响应式的呢

`Vue`为我们提供了一个`toRefs`的函数，可以将reactive返回的对象中的属性都转成ref；

那么我们再次进行结构出来的 name 和 height本身都是 ref的；

```js
// 那么解构出来的age 和height本身都是react
const { age, height } = toRefs(info)
```

#### `toRef`

如果我们只希望转换一个reactive对象中的属性为ref, 那么可以使用`toRef`的方法

```js
// 如果只想解构其中一个
const name = toRef(info, 'name')
```

#### ref的其他`api`

##### `unref`

如果我们想要获取一个ref引用中的value，那么也可以通过`unref`方法：

如果参数是一个 ref，则返回内部值，否则返回参数本身；

这是 `val = isRef(val) ? val.value : val` 的语法糖函数；

#####  `isRef`

判断值是否是一个ref对象。

#####  `shallowRef`

创建一个浅层的ref对象；

#####  `triggerRef`

手动触发和 `shallowRef` 相关联的副作用：

```js
const info = shallowRef({name:'abc'});
// 下面的方法修改不是响应式的
const changeInfo =()=>{
    info.value.name = 'cba'
    // 手动触发
    triggerRef(info)
}
```

