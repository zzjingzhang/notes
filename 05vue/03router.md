URL的hash

前端路由是如何做到URL和内容进行映射的呢？监听URL的改变

## URL的hash

URL的hash也就是锚点(#)，本质上是改变window.location的href属性

我们可以直接赋值location.hash来改变href，但是页面不发生刷新

```html
<div>
    <a href="#/home">home</a>
    <a href="#/about">about</a>
    <div class="router-view"></div>
</div>
```

```js
// 1.获取router-view
const routerViewEl = document.querySelector('.router-view')
// 2.监听hashchange
window.addEventListener('hashchange',()=>{
    switch(location.hash){
        case "#/home":
            reouterViewEl.innerHTML = 'home';
            break;
        case "#/about":
            routerViewEl.innerHTML = 'about';
            break;
        default:
            routerViewEl.innerHTML ='default'
    }
})
```

hash的优势就是兼容性更好，在老版本IE中都可以运行，但是缺陷是有一个#，显得不像一个真实的路径

## HTML5的history

history接口是HTML5新增的，它有六种模式改变URL而不刷新页面

replaceState:替换原来的路径

pushState:使用新的路径

popState:路径的回退

go:向前或向后改变路径

forward:向前改变路径

back:向后改变路径

```js
// 1.获取router-view
const routerViewEl = document.querySelector('.router-view')
// 2.监听所有a元素
const aEls = document.querySelector('a');
for(let aEl of aEls){
    aEl.addEventListener('click',e=>{
        e.preventDefault();
        const href = aEl.getAttribute('href');
        history.pushState({},"",href);
        historyChange()
    })
}
//3.监听popState和go操作
window.addEventListener('popState',historyChange);
window.addEventListener('go',historyChange);
// 4.执行设置页面操作
function historyChange(){
  switch(location.pathname){
    case "/home":
       reouterViewEl.innerHTML = 'home';
       break;
    case "/about":
       routerViewEl.innerHTML = 'about';
       break;
     default:
       routerViewEl.innerHTML ='default'
    } 
}
```

## vue-router

vue-router是vue的官方路由

vue-router的使用步骤

1.创建路由需要映射的组件（打算显示的页面）

2.通过createRouter创建路由对象，并且传入routes和history模式

​      配置路由映射：组件和路径映射关系的routes数组

​      创建基于hash或者history的模式

3.使用app注册路由对象（use方法）

4.路由使用通过\<router-link\>和\<router-view\>

### 基本使用

```js
import { createRouter, createWebHashHistory, createWebHistory } from "vue-router";
// 1.导入创建的组件
import Home from '../views/Home.vue'
import About from '../views/About.vue'
 // 2.配置路由的映射关系
const routes= [
   {path: '/home',component: Home },
   {path: '/about',component: About,}, 
  ],
  // 3.创建router对象
const router = creatRouter({
    routes,
    history:createWebHashHistory()
})
// 4.在main.js中注册路由
import { createApp } from 'vue'
import router from './router'
import App from './App.vue'

const app = createApp(App)
app.use(router)
app.mount('#app')
// 5.组件中使用
```

```html
<div>
  <h2>app</h2>
  <div class="nav">
    <router-link to="/home">首页</router-link>
     <!-- to属性也可以传一个对象 -->
     <!-- <router-link :to="{ path: 'home' }">首页</router-link> -->
     <router-link to="/about">关于</router-link>
    </div>
    <router-view></router-view>
  </div>
```

### 路由的默认路径

默认情况下，进入网址的首页，我们希望\<router-view\>渲染首页的内容，但是我们的实现中，默认没有显示首页组件，必须让用户点击才可以

可以通过redirect属性，重定向到首页

```js
const routes= [
   {path:'/',redirect:'/home'
   {path: '/home',component: Home },
   {path: '/about',component: About,}, 
  ],
```

### router-link

属性：

to属性：是一个字符串或者一个对象

replace属性：设置replace属性的话，当点击时，会调用router.replace(),而不是router.push()

active-class属性：设置激活a元素后应用的class,默认是router-link-active

exact-active-class属性：链接精准激活时，应用于渲染\<a\>的class，默认是router-link-exact-active（主要用于嵌套路由）

### 路由懒加载

当打包构建应用式，js包会变得非常大。影响页面加载

如果我们能把不同路由对应的组件分割成不同的代码块，然后当路由被访问的时候才加载对应的组件，这样就会更加高效

vue-router支持动态来导入组件，component可以传入一个组件，也可以接收一个函数，该函数需要返回一个promise

```js
const Home = () => import('../views/Home.vue')
const About = () => import('../views/About.vue')
const routes= [
   {path:'/',redirect:'/home'
   {path: '/home',component: Home },
   {path: '/about',component: About,}, 
  ],
```

### 路由的其他属性

name属性：路由记录独一无二的名称

meta属性：自定义的数据

### 动态路由基本匹配

很多时候我们需要将给定匹配模式的路由映射到同一个组件

例如，我们可能有一个user组件。它应该对所有用户进行渲染。但是用户的id是不同的，在vue-router中，我们可以在路径中使用一个动态字段来实现。我们称之为 路径参数

```js
 {
    path: '/user/:id', // 动态路由
    component: () => import('../views/User.vue')
   },
```

#### 获取动态路由的值

在template中，直接通过$route.params获取

在created中。通过this.$route.params获取

在setup中。我们要使用vue-router库给我们提供的一个hook useRoute

该hook会返回一个Route对象，对象中保存着当前路由相关的值

```js
import { useRoute } from 'vue-router'
// 获取route跳转id
const route = useRoute()
console.log(route.params.id)
```

### NotFound

对于那些没有匹配的路由。我们通常会匹配到固定的某个页面

```js
// 匹配不到对应的路由组件，显示找不到
        {
         path: '/:pathMatch(.*)', // /:pathMatch(.*) 和/:pathMatch(.*)* 的区别，后者会对路径做一个解析，解析为数组比如abc/cba/nba,会解析为['abc','cba','nba']
         component: () => import('../views/NotFound.vue')
        }
```

我们可以通过$route.params.pathMatch获取到传入的参数

### 路由的嵌套

```js
{
            path: '/home',
            name: 'home',  // name必须是唯一的
            component: Home,
            meta: {
                name: '',
                age: ''
            },
            children: [
                {
                    path: '/home',
                    redirect: '/home/recommend'
                },
                {
                    path: 'recommend', // 相当于 /home/recommend
                    component: () => import('../views/HomeRecommend.vue')
                },
                {
                    path: 'rank',
                    component: () => import('../views/HomeRank.vue')
                }
            ]
        },
```

### 动态添加路由

某些情况下，我们可能需要动态来添加路由

```js
// 动态添加一个一级路由 
router.addRoute({
        path: '/admin',
        component: () => import('../views/Admin.vue')
    })

// 如果我们是为route添加一个children路由，那么可以传入对应的name：
// 二级路由
    // 第一个参数是父级路由的名字
    router.addRoute('home', {
        path: 'vip',
        component: () => import('../views/homeVip.vue')

    })
```

#### 动态管理路由的其他方法

删除路由有以下三种方式

1.添加一个name相同的路由

2.通过removeRoute方法。传入路由的名称

3.通过addRoute方法的返回值回调

### 路由其他方法补充

router.hasRoute():检查路由是否存在

router.getRoutes():获取一个包含所有路由记录的数组

### 路由导航守卫

vue-router提供的导航守卫主要用来通过跳转或取消的方式守卫导航

全局的前置守卫beforeEach是在导航触发时会被回调的

它有两个参数：

to:即将进入的路由route对象

from：即将离开的路由Route对象

它有返回值：

false：取消当前导航

不返回或者undefined：进行默认导航

返回一个路由地址：可以是一个string类型的路径；可以是一个对象，对象中包含path、query、params等信息

可选的第三个参数：next（不推荐）