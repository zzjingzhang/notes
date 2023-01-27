# jQuery

## 1.什么是CDN

CDN称之为内容分发网络(Content Delivery Network 或Content Distribution Network,缩写CDN)

- CDN它是一组分布在不同地理位置的服务器相互连接形成的网络系统
- 通过这个网络系统，将web内容存放在距离用户最近的服务器
- 可以更快、更可靠的将web内容(文件、图片、音乐、视频等)发送给用户
- CDN不但可以提高资源的访问速度，还可以分担源站的压力

## 2.jQuery安装方式

1.CDN引入

```html
  <!-- 
    integrity： 作用防止资源被篡改，如果资源被篡改那么浏览器将不会下载该资源
    crossorigin：加载 不同源 的资源时是否需要携带用户凭证信息（cookie 、 ssl证书..）
         值为 anonymous、‘’ 或者不写代表是：不需要携带 。
         值为 user-credentail : 代表获取该资源时需要携带用户凭证信息。
   -->

<script src="https://code.jquery.com/jquery-3.6.0.js" integrity="sha256-H+K7U5CnXl1h5ywQfKtSj8PCmoN9aaq30gDh27Xc0jk=" crossorigin="anonymous"></script>


<!--  执行下面代码，会做哪些事情：
1.在window里面新加一个jQuery函数，window.jQuery
2.在window里面新加一个$函数，window.$ 
两个函数指向同一个工厂函数
-->
<script src="https://code.jquery.com/jquery-3.6.0.js"></script>
```

2.下载源码引入

3.npm安装

## 3.jQuery监听文档加载

```js
  //  监听html文档完全解析完成
//  监听document的DOMContentLoaded事件

        // 方式一
        // $(document).ready(function () {
        //     console.log('ready 方式一')
        // })

        // 方式二
        // $('document').ready(function () {
        //     console.log('ready 方式二')
        // })

        // 方式三
        // $().ready(function () {
        //     console.log('ready 方式三')
        // })

        // 方式四(推荐)
        $(function () {
            console.log('ready 方式四')
        })
```

```js
// 监听window的load事件,即网页所有资源(外部链接，图片等)加载完成

// .load(handler) // 这个api在jQuery3.0被移除了

$(window).on('load',handler)  // 推荐写法
```

## 4.jQuery与其它库的变量名冲突

在 jQuery 中，$ 是jQuery的别名。
如果我们在使用jQuery库之前，其它库已经使用了 $ 函数或者变量，这时就会出现冲突的情况。
这时我们可以通过调用jQuery中的noConflict函数来解决冲突问题。
jQuery在初始化前会先备份一下全局其它库的jQuery和$变量，调用noConflict函数只是恢复之前备份的jQuery和$变量

```js
// jQuery解决变量冲突的源码
var
	// Map over jQuery in case of overwrite
	_jQuery = window.jQuery, // 备份其它库的相同变量

	// Map over the $ in case of overwrite
	_$ = window.$; // 备份其它库的相同变量
jQuery.noConflict = function( deep ) {
	if ( window.$ === jQuery ) {
		window.$ = _$; // 恢复
	}

	if ( deep && window.jQuery === jQuery ) {
		window.jQuery = _jQuery;  // 恢复
	}

	return jQuery;  // 返回一个jQuery函数
};

// 解决冲突，调用一下noConflict函数即可
const newJQuery = jQuery.noConflict(true)
```

