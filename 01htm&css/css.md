# CSS

#### 结构伪类-

##### :nth-child()

###### :nth-child(1)

- 是父元素中的第一个子元素

###### :nth-child(2n)

- n代表正整数和0
- 是父元素中的第偶数个子元素(第2、4、6....个)
- 跟:nth-child(even)同义 

###### :nth-child(2n+1)

- n代表正整数和0
- 是父元素中的第奇数个子元素(第1、3、5....个)
- 跟:nth-child(odd)同义 

###### **:nth-child(-n+2)**

- 代表前两个子元素

##### :nth-last-child()

:nth-last-child()语法跟:nth-child()类似，不同点是:nth-last-child()从最后一个元素开始往前计数

:nth-last-child(1),代表倒数第一个元素

:nth-last-child(-n+2),代表倒数第二个元素

### 定位

##### 相对定位-relative

- 元素按照标准流布局
- 可以通过**left right top bottom**进行定位
- 定位**参照对象**是元素**自己原来的位置**

**相对定位的应用场景**

在**不影响其他元素位置的前提**下，对**当前元素位置进行微调**

##### 固定定位-fixed

- 元素**脱离标准流**
- 可以通过**left right  bottom to**p进行定位
- 定位参照对象是视口(viewport)
- 当画布滚动时，固定不动

###### 视口

- 文档的可视区域

###### 画布

- 用于渲染文档的区域
- 文档内容超出视口范围，可以滚动查看

宽高对比

**画布>=视口**

##### 绝对定位 - absolute

**元素脱离文档流**

**可以通过left bottom top right进行定位**

- 定位参照对象是最邻近的定位祖先元素
- 如果找不到这样的祖先元素，参照对象是视口

**定位元素**

- position值不为static
- 也就是position的值为relative、absolute、fixed的元素

##### 将position设置为absolute/fixed元素的特点(一)

- 可以随意设置宽高

- 宽高默认由内容决定

- 不再受标准流的约束

   不再严格按照从上到下、从左到右排布

   不再严格区分块级、行内级、行内块级的很多特性都会消失

- 不再给父元素汇报宽高数据

- 脱标元素内部默认还是按照标准流布局

##### 将position设置为absolute/fixed元素的特点(二)

- 绝对定位元素(absolutely positioned element)

​        position的值为**absolute** 或者 **fixed**的元素

- 对于绝对定位元素来说

​              定位参照对象的宽度 = left + right +margin-left +margin-right+绝对定位元素的实际占用宽度

​              定位参照对象的高度 = top + bottom +margin-top +margin-bottom+绝对定位元素的实际占用高度

- 如果希望绝对定位元素的宽高和定位参照对象一样，可以给绝对定位元素设置以下属性

  ```css
  left:0;
  right:0;
  top:0;
  bottom:0;
  margin:0;
  ```

- 如果希望绝对定位元素在定位参照对象中居中显示，可以给绝对定位元素设置以下属性

    另外，还得**设置具体的宽高值**(宽高小于定位参照对象的宽高)

  ```css
  left:0;
  right:0;
  top:0;
  bottom:0;
  margin:auto;
  ```

```html
   .box{
      position: relative;
      background-color: red;
      width: 1000px;
      height: 400px;
    }
    .sub-box{
      position: absolute;
      width: 300px;
      height: 100px;
      background-color:blue;
      left: 0;
      right: 0;
      top:0;
      bottom: 0;
      margin:auto;
    }
  <div class="box">
    <div class="sub-box"></div>
  </div>

```

##### 粘性定位-sticky

- 可以看做是**相对定位和绝对定位的结合体**
- 它允许被定位元素**表现得像相对定位一样**，直到它滚动到某个阈值点
- 当**达到这个阈值点**时，就会**变成固定定位**
- sticky是相对于最近的滚动祖先包含滚动视口的

##### z-index

**z-index属性用来设置元素的层叠顺序(仅对定位元素有效)**

取值可以是正整数、负整数、0

**比较原则**

- 如果是兄弟关系

​            z-index越大，层叠在越上面

​            z-index相等，写在后面的那个元素层叠在上面

- 如果不是兄弟关系

​              各自从元素自己以及祖先元素中，找出最邻近的2个定位元素进行比较

​              而且这两个定位元素必须设置z-index的具体数值

### 浮动

##### 浮动的问题-高度塌陷

由于浮动元素脱离了标准流，变成了脱标元素，所以不再向父元素汇报高度

父元素计算总高度时，就不会计算浮动子元素的高度，导致了**高度塌陷**的问题

##### 清浮动

清浮动的目的是

让父元素计算总高度的时候，把浮动子元素的高度算进去

清除浮动：使用clear属性

##### css属性-clear

clear属性可以指定一个元素是否必须移动（清除浮动后）到在它之前的浮动元素下面

clear的常用值

- left：要求元素的顶部低于之前生成的所有左浮动元素的底边
- right：要求元素的顶部低于之前生成的所有右浮动元素的底部
- both：要求元素的顶部低于之前生成的所有浮动元素的底部
- none：默认值，无特殊要求

##### 清除浮动的方法：

1.给父元素设置固定高度（不推荐）

2.在父元素最后增加一个空的块级子元素，并且让它设置clear:both（不推荐）

​    弊端:会增加很多无意义的空标签。维护麻烦

​            违反了结构与样式分离的原则

3.给父元素添加一个伪元素（推荐）

```css

.clear-fix::after{
    content:'';
    display:block;
    clear:both;
    
    visibility:hidden; /* 浏览器兼容性 */
    height:0;/* 浏览器兼容性 */
}
.clear-fix{
    *zoom:1;  /* IE6/7兼容性 */
}
```

### flex

**flex布局的两个重要概念**

1.开启了flex布局的元素叫做flex container

2.flex container里面的直接子元素叫做flex item



**当flex container 中的子元素变成了flex item 时，具备以下特点**

- flex item的布局将受flex container 属性的设置来进行控制和布局
- flex item不再严格区分块级元素和行内级元素
- flex item 默认情况下是包裹内容的，但是可以设置宽高

 

#### flex相关的属性

##### 应用在flex container上的css属性

###### flex-direction

**flex items 默认都是沿着main aixs（主轴）从main start 开始往main end方向排布**

flex-direction 决定了 main axis的方向，有四个取值

**row（默认值）**、row-reverse、column、column-reverse

###### flex-wrap

**flex-wrap决定了flex-container是单行还是多行**

- nowrap（默认）：单行
- wrap：多行
- wrap-reverse：多行（对比wrap，cross start 与 cross end 相反）

###### flex-flow

flex-flow属性是flex-direction 和 flex-wrap的简写

顺序任意，并且都可以省略

###### justify-content

**justify-content 决定了flex items 在main axis上的对齐方式**

- flex-start（默认值）：与main start对齐
- flex-end：与main end对齐
- center：居中对齐
- space-between： 1.flex items之间距离相等 2.与main start 、main end两端对齐
- space-around： 1.flex items之间距离相等 2.flex items与main start 、main end之间的距离是flex items之间距离的一半
- space-evenly： 1.flex items之间距离相等 2.flex items与main start 、main end之间的距离等于flex items之间的距离

###### align-items

align-items决定了flex items在cross axis（交叉轴）上的对齐方式

- normal：在弹性布局中，效果和stretch一样
- stretch：当flex items在cross axis方的size为auto时，会自动拉伸至填充flex container
- flex-start：与cross start对齐
- flex-end：与cross end对齐
- center：居中对齐
- baseline：与基准线对齐

###### align-content

align-content决定了多行flex items在cross axis上的对齐方式，用法与just-content类似

- stretch（默认值）：与align-items的stretch类似
- flex-start：与cross start对齐
- flex-end：与cross end对齐
- center：居中对齐
- space-between： 1.flex items之间距离相等 2.与cross start 、cross end两端对齐
- space-around： 1.flex items之间距离相等 2.flex items与cross  start 、cross end之间的距离是flex items之间距离的一半
- space-evenly： 1.flex items之间距离相等 2.flex items与cross start 、cross end之间的距离等于flex items之间的距离

##### 应用在flex items上的css属性

###### flex-grow

**flex-grow决定了flex items如何扩展（拉伸/成长）**

- 可以设置任意非负数字（正小数、正整数、0），默认值是0
- 当flex container在main axis方向上有剩余size时，flex-grow才会有效

**如果所有flex items的flex-grow总和sum超过1，每个flex item扩展的size为 ： flex container的剩余size*flex-grow/sum**

**flex items扩展后的最终size不能超过max-width\max-height**

###### flex-basis

flex-basis用来设置flex items在main axis方向上的base size

auto（默认值）、具体的宽度数值

决定flex items最终base size的因素，从优先级高到低

- max-width\max-height\min-width\min-height
- flex-basis
- width\height
- 内容本身的size

###### flex-shrink

**flex-shrink决定了 flex items如何缩写（收缩）**

- 可以设置任意非负数字（正小数、正整数、0），默认值是1
- 当flex items在main axis方向上超过了flex container的size时，flex--shrink才会有效

**如果所有flex items的flex-shrink总和超过1，每个flex item收缩的size为 ：**

-  flex items超出flex container的size*收缩比例 / 所有flex items的收缩比例之和

**flex items收缩后的最终size不能小于min-width\min-height**

###### order

**order决定了flex items的排布顺序**

- 可以设置任意整数（正整数、负整数、0），值越小就越排在前面
- 默认值是0

###### align-self

**flex items可以通过align-self覆盖flex container设置的align-items**

auto（默认值）：遵从flex container 的align-items设置

stretch、flex-start、flex-end、center、baseline，效果和align-item是一致

###### flex

flex是flex-grow || flex-shrink || flex-basis的简写，flex属性可以指定1个2个或3个值

**单值语法：值必须为以下其中一个**

- 一个无单位数：它会被当做flex-grow的值
- 一个有效的宽度值：它会被当做flex-basis的值

- 关键字none，auto或initial

**双值语法：第一个值必须为一个无单位数，并且会被当做flex-grow的值**

第二个值必须为以下之一

- 一个无单位数：它会被当为flex-shrink的值
- 一个有效的宽度值：会被当做flex-basis的值

**三值语法**

- 第一个值必须为一个无单位数：它会被当为flex-grow的值
- 第二个值必须为一个无单位数：它会被当为flex-shrink的值
- 第三个值必须为一个有效的宽度值：它会被当为flex-basis的值

### 形变

#### CSS属性-transform

css transform属性允许对某一个元素进行某些形变，包括旋转，缩放，倾斜或平移等

注意：并非所有的盒子都可以进行transform的转换（通常行内级元素不能进行形变）

常见 函数Transform function有：

- 平移：translate(x,y)
- 缩放：scale(x,y)
- 旋转：rotate(deg)
- 倾斜：skew(deg,deg)

##### 位移-translate

平移：translate(x,y)

这个css函数用于移动元素在平面上的位置

值个数

- 一个值时，设置x轴上的位移
- 二个值时，设置x轴和y轴上的位移

值类型

- 数字：100px
- 百分比：参照元素本身

应用设置居中

```html
  <style>
    .container{
      height: 500px;
      background-color: #f00;
    }
    .box{
      height: 200px;
      position: relative;
      top:50%;
      transform: translateY(-50%);
      background-color: blue;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="box"></div>
  </div>

</body>
```

###### translate的补充

- 1.translate是translateX和translateY函数的简写
- 2.translate的百分比可以完成一个元素的水平和垂直居中

##### 缩放-scale

scale() CSS函数可以改变元素的大小

值个数

- 一个值时，设置x轴上的缩放
- 两个值时，设置x轴和y轴上的缩放

值类型

- 数字：1：保持不变；2：放大两倍；0.5：缩小一半
- 百分比：百分比不常用

scale函数是scaleX 和scaleY的缩写

##### 旋转-rotate

**值个数**

- 一个值时，表示旋转的角度

**值类型**

- 常用单位deg：旋转的角度
- 正数为顺时针
- 负数逆时针

**注意：旋转原点受transform-origin的影响**

##### transform-origin

形变的原点

比如在进行scale缩放或者rotate旋转时，都会有一个原点

- 一个值：设置x轴的原点
- 两个值：设置x轴和y轴的原点

**必须是\<length>,\<percentage>或left，center，right，top，bottom关键字中的一个**

- left，center，right，top，bottom关键字
- length：从左上角开始计算
- 百分比：参考元素本身大小

```css
transform-origin:top left
```

![image-20220912125259154](C:\Users\10244\AppData\Roaming\Typora\typora-user-images\image-20220912125259154.png)

##### 倾斜-skew

skew()函数定义了一个元素在二维平面上的倾斜转换

**值个数**

- 一个值：表示x周轴上的倾斜
- 两个值：表示x轴和y轴上的倾斜

**值类型**

deg：倾斜的角度

正数为顺时针

负数为逆时针

**注意：倾斜的原点受transform-origin的影响**

transform设置多个值

transform可以设置多个形变函数

```css
.box{
    width:200px;
    height:200px;
    background-color:#f00;
    transform:translate(100px) scale(0.5) rotate(45deg)
}
```

#### transition动画

CSS transitions提供看一种在更改css属性时控制动画速度的方法

可以让css属性变化成为一个持续一段时间的过程，而不是立即生效的

比如将一个元素从一个位置移动到另一个位置，默认在修改完css属性后会立即生效

但是 我们可以通过才css transition，让这个过程加上一定的动画效果，包括一定的曲线速率变化

通常将两个状态之间的过渡称为隐式过渡，因为开始与结束之间的状态由浏览器决定

CSS transition 可以决定

- 哪些属性发生动画效果
- 何时开始(设置delay)
- 持续多久(设置duration)
- 如果动画(定义timing function，比如匀速地或先快后慢)

transition CSS属性是transition-property，transition-duration，transi-timing-func和transition-delay的一个简写属性

###### transition-property

指定应用过渡属性的名称

- all:所有的属性都执行动画
- none:所有的属性都不执行动画
- CSS属性名称：要执行动画的CSS属性名称，比如width left transform等

###### transition-duration

指定过渡动画所需时间

- 单位可以是秒或毫秒

###### transition-timing-function

指定动画的变化曲线

###### transition-delay

指定过渡动画执行之前的等待时间

#### animation

###### transition过渡动画的缺点

- 1.transition只能定义开始状态和结束状态，不能定义中间状态
- 2.transition不能重复执行，除非一再触发动画
- 3.transition需要在特定状态下触发才能执行

##### animation动画的使用步骤

- 1.使用keyframes定义动画序列
- 2.配置动画执行的名称、持续时间、动画曲线、延迟、执行次数、方向等

###### @keyframe规则

可以使用@keyframe来定义多个变化状态，并且使用animation-name来声明匹配

- 关键帧使用percentage来指定动画发生的时间点
- 0%表示动画的第一时刻，100%表示动画的最终时刻
- 因为这两个时间点十分重要，所以还有特殊的别名 from 和 to
- from 相当于1%
- to相当于100%

```css
  <style>
    .box {
      width: 200px;
      height: 100px;
      background-color: orange;

      /* box要执行moveAnim的动画 */
      animation-name: moveAnim;
      animation-duration: 3s;
      animation-timing-function: ease-in-out;

      /* 其他属性: */
      /* 动画执行的次数 */
      /* animation-delay: 2s; */
      /* animation-iteration-count: 2; */
      /* animation-direction: reverse; */
      /* 元素停留在动画的哪一个位置 */
      /* animation-fill-mode: forwards; */

      /* js动态修改 */
      /* animation-play-state: paused; */
      animation: moveAnim 3s linear 1s 2 normal forwards, ;
    }

    @keyframes moveAnim {
      0% {
        transform: translate(0, 0) scale(0.5, 0.5);
      }

      33% {
        transform: translate(0, 200px) scale(1.2, 1.2);
      }

      66% {
        transform: translate(400px, 200px) scale(1, 1);
      }

      100% {
        transform: translate(400px, 0) scale(0.5, 0.5);
      }
    }
  </style>
```

##### animation属性

animation属性是animation-name，animation-duration，animation-timing-function，animation-dealy。animation-iteration-count，animation-direction，animation-fill-mode和animation-play-state属性的一个简写属性

- animation-name：指定执行哪一个关键帧动画，

- animation-duration：指定动画的持续时间，

- animation-timing-function：指定动画的变化曲线，

- animation-dealy：指定延迟执行的时间，

- animation-iteration-count：指定动画执行的次数，执行infinite表示无限动画，

- animation-direction：指定方向，常用值normal和reverse，

- animation-fill-mode：执行动画最后保留哪一个值

    none:回到没有执行动画的位置

    forwards:动画最后一帧的位置

    backwards:动画第一帧的位置

- animation-play-state：指定动画运行或暂停

### 深入理解vertical-align  

#### line-boxes

官方文档的翻译：vertical-align会影响行内块级元素在一个行盒中垂直方向的位置

刚高为什么可以撑起div高度

这是因为vertical-align的存在，并且line-boxes有一个特性，包裹每行的inline level

而其中的文字是有行高的，必须将整个行高包裹进去，才算包裹这个line-level

#### 不同情况分析

1.只有文字时  line boxes如果包裹内容（注意：红色是包裹的div，下面也都一样）

![image-20220912160910523](C:\Users\10244\AppData\Roaming\Typora\typora-user-images\image-20220912160910523.png)

2.有图片，有文字时，line-boxes如何包裹内容

![image-20220912160933463](C:\Users\10244\AppData\Roaming\Typora\typora-user-images\image-20220912160933463.png)

3.有图片，有文字，有inline-block(比图片要大)如果包裹内容

![image-20220912160957407](C:\Users\10244\AppData\Roaming\Typora\typora-user-images\image-20220912160957407.png)

4.有图片，有文字，有inline-block(比图片要大)而且设置了margin-bottom，如何包裹?

![image-20220912161150143](C:\Users\10244\AppData\Roaming\Typora\typora-user-images\image-20220912161150143.png)

5.有图片，有文字，inline-block(比图片要大)而且设置了margin-bottom并且有文字，如果包裹内容

![image-20220912161217835](C:\Users\10244\AppData\Roaming\Typora\typora-user-images\image-20220912161217835.png)

#### vertical-align的baseline

结论:line-boxes一定会想办法包裹住当前行中的所有的内容

但是，为什么对齐方式千奇百怪呢？

你认为的千奇百怪，其实有它内在规律

答案就是baseline对齐

vertical-align的默认值就是baseline

但是baseline都是谁呢？

- 文本baseline是字面x的下方
- inline-block默认的baseline是margin-bottom的底部
- inline-block有文本时，baseline是最后一行文本x的下方

## HTML5新增元素

### HTML5新增了语义化的元素

header：头部元素

nav：导航元素

section：定义文档某个区域的元素

article：内容元素

aside：侧边栏元素

footer：尾部元素

### HTML5增加了对媒体类型的支持

音频：audio

视频：video

#### video

video元素用于在html或xhtml文档中嵌入媒体播放器，用于支持文档内的视频播放

##### video常见的属性

![image-20220912165953800](C:\Users\10244\AppData\Roaming\Typora\typora-user-images\image-20220912165953800.png)

##### video的兼容性写法

1：通过source元素指定更多视频格式的源

2.通过p/div元素指定在浏览器不支持video的情况下，显示的内容

```html
<video src="../video/fcrs.mp4" controls autoplay muted>
    <source src="../video/frcs.webm">
    <p>
        你的浏览器不支持视频播放，请更换浏览器查看
    </p>
</video>
```

#### audio

audio元素用于在文档中嵌入音频内容，和video的用法非常类似

##### audio常见属性

![image-20220912170536011](C:\Users\10244\AppData\Roaming\Typora\typora-user-images\image-20220912170536011.png)

在audio元素中间的内容，是针对浏览器不支持此元素时候的降级处理

```html
<audio src="../media/yhbk.mp3" controls autoplay muted>
    <source src="../media/yhbk.ogg">
    <p>
        你的浏览器不支持音频播放，请更换浏览器查看
    </p>
</audio>
```

### input元素的扩展内容

HTML5对input元素也进行了扩展

date

time

number

tel

color

email

### 新增全局属性data-*

在HTML5中，新增一种全局属性格式data-*，用于自定义数据属性

- data设置的属性可以在js的DOM操作中通过dataset轻松获取到
- 通常用于HTML和js数据之间的传递

```html
<div class="box" title="abc" data-name="why" data-age="18"></div>
<script>
    const boxEL= document.querySelector('.box')
    console.log(boxEL.dataset)
</script>
```

- 在小程序中，就是通过data-来传递数据的

### CSS属性 white-space

**white-space用于设置空白处理和换行规则**

- normal:合并所有连续空白，允许单词超屏时自动换行
- nowrap:合并所有连续的空白，不允许单词超屏时自动换行
- pre:阻止合并所有连续的空白，不允许单词超屏时自动换行
- pre-wrap:阻止合并所有连续的空白，允许单词超屏时自动换行
- pre-line:合并所有连续的空白(但保留换行)，允许单词超屏时自动换行

### CSS属性-text-overflow

**text-overf通常用来设置文字溢出时的行为**

- clip:溢出的内容直接裁剪掉（字符可能会显示不完整)
- ellipsis:溢出的那行的结尾处用省略号表示



**text-overflow生效的前提是overflow不为visible**

### CSS中的函数

- var:使用CSS定义的变量
- calc:计算CSS的值，通常用于计算元素的大小或位置
- blur:高斯模糊效果
- gradient:颜色渐变函数

#### CSS函数-var

css中可以自定义属性

- 属性名需要以两个减号(--)开始
- 属性值可以是任何有效的CSS值

```css
div{
    --main-color:red;
}
```

可以通过var函数来使用

```css
span{
    color:var(--main-color)
}
```

#### CSS函数-calc

calc()函数允许声明css属性值是执行一些计算

计算支持加减乘除的匀运算

加号和减号运算符的两边必须要有空白字符

通常用来设置一些元素的尺寸会位置

```css
.container{
    display:inline-block;
    width:calc(100% - 60px);
}
```

#### CSS函数-blur

**blur()函数将高斯模糊应用于输出图片或者元素**

- blur(radius)
- radius:模糊的半径，用于定义高斯函数的偏差值，偏差值越大，图片越模糊

**通常会和两个属性一起使用**

- filter:将模糊或颜色偏移等图形效果应用于元素
- backdrop-filter:为元素后面的区域添加模糊或者其他效果

#### CSS函数-gradient

gradient是一种image CSS数据类型的子类型，用于表现两种或多种颜色的过渡转变

- CSS的image数据类型描述的是2D图形
- 比如background-image，list-style-image，border-image，content等
- image常见的方式是是通过url引入一个图片资源
- 它也可以通过CSS gradient函数来设置颜色的渐变

**gradient常见的函数实现有下面几种**

- linear-gradient()：创建一个表示两种或多种颜色线性渐变的图片

```css
background-image:linear-gradient(blue,red);

background-image:linear-gradient(to right,blue,red);

background-image:linear-gradient(to right bottom,blue,red);

background-image:linear-gradient(45deg,blue,red);

background-image:linear-gradient(to right,blue,red 10%,purple 40px,orange);
```



- radial-gradient():创建了一个图像，该图像是由从原点发出的两种或者多种颜色之间的逐步过渡组成

  ```css
  background-image:radial-gradient(blue,red);
  ```

  ![image-20220912184115709](C:\Users\10244\AppData\Roaming\Typora\typora-user-images\image-20220912184115709.png)

  ```css
  background-image:radial-gradient(at 0% 50%,red,yellow);
  ```

  ![image-20220912184208531](C:\Users\10244\AppData\Roaming\Typora\typora-user-images\image-20220912184208531.png)

- repeating-linear-gradient():创建一个重复性渐变组成的\<image>

- repeating-radial-gradient():创建一个重复的原点触发渐变组成的\<image>

### FC-Formatting Context

什么 是FC？

FC的全称是Formatting Context ，元素在标准流里面都是属于一个FC的

**块级元素的布局属于Bloc Formatting Context(BFC)**

- 也就是block level box都是在BFC中布局的

**行内及元素的布局属于inline Formatting Context(IFC)**

- 而inline level box都是IFC中布局的

#### BFC

BFC的作用

- 在BFC中，box会在垂直方向上一个挨着一个的排布
- 垂直方向的间距由margin决定
- 在同一个BFC中，相邻两个box之间的margin会折叠
- 在BFC中，每个元素的左边缘是紧挨着包含块的左边缘

BFC有什么用呢？

- 解决margin的折叠问题

 在同一个BFC中，相邻两个box之间的margin会折叠

那么如果我们让这两个box是不同的BFC呢？那么就可以解决折叠问题了

- 解决浮动高度塌陷问题

BFC解决高度塌陷需要满足两个条件

浮动元素的父元素触发BFC，形成独立的块级格式化上下文

浮动元素的父元素的高度是auto

**BFC的高度auto的情况下，是如下方法计算高度的**

- 1.如果只有inline-leve，是行高的顶部和底部的距离
- 2.如果有block-level，是由最底层的块上边缘和最底层块盒子的下边缘之间的距离
- 3.如果有绝对定位元素，将被忽略
- 4.**如果有浮动元素，那么会增加高度以包括这些浮动元素的下边缘**

### 媒体查询

#### 媒体查询的使用方式有三种

1.通过@media和@impor使用不同的CSS规则（常用）

```css
@import url(./css/miniScreen.css) (max-width:600px);
```

2.使用media属性为\<style>,\<link>,\<source>和其他HTML元素指定特定的媒体类型

```html
<link rel="stylesheet" media="(max-width:600px)" href="./css/miniScreen.css">
```

3.使用window.matchMedia()和MediaQueryList.addListener()方法来测试和监控媒体状态

##### 媒体查询-媒体类型(Media type)

在使用媒体查询时，必须指定要使用的媒体类型

媒体类型是可选的，并且会(隐式地)应用all类型

常见媒体类型值如下

all:使用于所有设备

print:适用于在打印预览模式下载屏幕上查看的分页材料和文档

**screen:主要用于屏幕**

speech:主要用于语音合成器

##### 媒体查询-媒体特性(Media features)

媒体特性描述了浏览器、输出设备、或是预览环境的具体特征

- 通常会将媒体特性描述为一个表达式
- 每天媒体特性表达式都必须用括号括起来

![image-20220912212506740](C:\Users\10244\AppData\Roaming\Typora\typora-user-images\image-20220912212506740.png)

##### 媒体查询-逻辑操作符

**媒体查询的表达式最终会活动一个Boolean值，也就是true或false**

- 如果结果为true，那么就会生效
- 如果结果为false，那么就不会生效

**如果有多个条件，我们可以通过逻辑操作符联合复杂的媒体查询**

- and:and操作符用于将多个媒体查询规则组合成单条媒体查询
- not:not运算符用于否定媒体查询，如果不满足这个条件则返回true，否则返回false
- only:only运算符仅在整个查询匹配时才应用于样式
- ,(逗号):逗号多用于将多个媒体查询合并为一个规则

```css
/* 屏幕宽度大于500，小于700的时候，body背景颜色为红色*/
@media screen and (min-width:500px) and (max-width:700px){
    body{
        background-color:#f00;
    }
}
```

### CSS中的单位

css中的单位整体可以分为两类

绝对长度单位

相对长度单位

#### CSS中的绝对单位(Absolute length units)

绝对单位

- 他们与其他任何东西都没有关系，通常被认为总是相同的大小
- 这些值中的大多数在用于打印时比用于屏幕输出时更有用
- 前端开发经常使用的绝对单位就是px(像素)

![image-20220912222535889](C:\Users\10244\AppData\Roaming\Typora\typora-user-images\image-20220912222535889.png)

#### CSS中的相对单位(Relative length units)

相对长度单位

- 相对长度单位相对其他一些东西
- 比如父元素的字体大小，或者视图端口的大小
- 使用相对单位的好处是，经过一些仔细的规划，可以使文本或其他元素的大小与页面上的其他内容相对应

![image-20220912222822652](C:\Users\10244\AppData\Roaming\Typora\typora-user-images\image-20220912222822652.png)

#### 当我们在聊pixel时，到底在聊什么

**px是pixel单词的缩写，翻译为像素**

像素到底是什么呢？

- 像素 影响显示的基本单位（比如屏幕上看到的画面，一副图片）
- pix是英语单词picture的常用简写，加上英语单词‘元素’element，就得到pixel
- “像素”表示“画像元素”之意,有时也被称为pel(picture element)

##### 像素的不同分类

像素单位常见的有三种像素名称

- 设备像素（也称之为物理像素）
- 设备独立像素（也称之为逻辑像素）
- css像素

##### 物理像素和逻辑像素

设备像素，也叫物理像素

- 设备像素指的是显示器上的真实像素，每个像素的大小是屏幕固有的属性，屏幕出场以后就不会改变了
- 我们 购买显示器或者手机的时候，提到的设备分辨率就是设备像素的大小
- 比如iPhoneX的分辨率是1125*2436.指的就是设备像素

设备独立像素，也叫逻辑像素

- 如果面向开发者我们使用设备像素显示一个100px的宽度，那么在不同屏幕上显示的效果会是不同的
- 开发者针对不同的屏幕很难进行较好的适配，编写程序必须了解用户的分辨率来进行开发
- 所以在设备像素之上，操作系统为开发者进行抽象，提供了逻辑像素的概念
- 比如 你购买了一台显示器，在操作系统上市以1920*1080设置的分辨率，那么无论你购买的是2k、4k的显示器，对于开发者来说，都是1920*1080

CSS像素

- CSS中我们经常使用的单位也是pixel，它在默认情况下等同于设备独立像素（也就是逻辑像素）
- 毕竟逻辑像素才是面向我们开发者的

**我们可以通过js中的screen.width 和 screen.height获取到电脑的逻辑分辨率**

##### DPR、 PPI

###### DPR:device pixel ratio

- 2010年，iPhone4问世，不仅带来了移动互联网，还带来了Retina屏幕
- Retina屏幕翻译为视网膜显示屏，可以为用户带来更好的显示
- 在Retina屏幕中，一个逻辑像素在长度上对应两个物理像素，这个比例称之为设备像素比（device pixel ratio）
- 我们可以通过window.devicePixelRatio获取到当前屏幕上的DPR值

###### PPI:每英寸像素（英语：Pixel Per Inch。缩写PPI)

- 通常用来表示一个打印图像或者显示器上像素的密度
- 1英寸 = 2.54厘米，在工业领域被广泛应用

### CSS预处理器

社区为了解决CSS面临的大量问题，出现了一系列的CSS预处理器（CSS_preprocessor）

CSS预处理器是一个