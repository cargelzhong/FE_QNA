## Why not iframe

浏览器原生的样式、js 隔离，隔离性导致应用间上下文无法被共享

1. url 不同步。浏览器刷新 iframe url 状态丢失、后退前进按钮无法使用。
2. UI 不同步，DOM 结构不共享。想象一下屏幕右下角 1/4 的 iframe 里来一个带遮罩层的弹框，同时我们要求这个弹框要浏览器居中显示，还要浏览器 resize 时自动居中..
3. 全局上下文完全隔离，内存变量不共享。iframe 内外系统的通信、数据同步等需求，主应用的 cookie 要透传到根域名都不同的子应用中实现免登效果。
4. 加载慢。每次子应用进入都是一次浏览器上下文重建、资源重新加载的过程

## 双向绑定原理及实现

监听器（Observer）收集监听数据属性，消息订阅器（Dep）收集订阅者，数据发生变化的时候发布消息通知订阅者，然后解析器（Compiler）通知更新视图。 Object 的 definedPorperty() 便利属性值数据劫持，代理所有数据的 getter 和 setter，在 setter 触发时通知订阅者。

## 路由懒加载

使用()=>import ('../../xxx.vue') 形式，利用函数只有被调用才会执行，打包不同组件至不同 js，只有在进入当前路由才会加载对应的组件。

## vue-router 中 hash 模式和 h5 模式 区别

- 哈希模式：使用了哈希字符 "#" ,`Hash变化不会重新请求向服务器请求` 不需要再服务器层面做配置处理。SEO（搜索引擎优化）中表现较差。hashchange 事件触发
- H5 模式：容易出现刷新页面 404，需要服务端做重定向配置。

## 组件传参方式

- 父传子 props
- 子传父$emit 事件传参
- 共用数据源 vuex
- 事件总线 基于发布订阅模式 $emit $on $off

## cookie，sessionStorage，localStorage，vuex 区别

- cookie 一般是服务器创建后返回给浏览器，告诉浏览器设置 cookie 保存用户的信息。
- sessionStorage 是临时保存，页面被关闭就会清除，被限制在同个窗口，只能存字符串。
- localStorage 以文件形式本地永久保存，只能存字符串。
- vuex 状态管理器更多用于 vue 组件之间传值，多组件使用同一数据源的清空，是响应式的
  根据具体业务情况进行选择

## 什么时候需要函数封装

看过一个比喻，一行行代码就是一个个单词，各种词语组成了清楚表达某种明确含义的句子，就是应该封装函数的时候

## 单页面和非单页面的区别

- 非单页面是多个 html，跳转也是不同 html 间的跳转，首屏加载稍快，传参比较麻烦。
- 单页面就是只有一个 html 页面，较复杂的系统首屏加载会慢一些，一次请求了所有需要的资源，需要做优化处理，优点是加载完成后，页面切换较快，局部刷新用户体验较好。

## js 原型链

所有的原型构成了一个链条，这个链条我们称之为原型链（prototype chain)，主要是为了实现对象的继承，一般原型链的顶点是 Object.prototype。

## 判断变量是否是一个数组

const a = []

- Array.isArray(a); // true
- Object.prototype.toString.call(a) === '[object Array]'; // true

## 线程 进程

js 是单线程语言，宿主环境的多线程使它具有了异步的属性，浏览器才是真正实现异步的元凶。
js 不断从任务队列里提取任务到主线程执行，

## 浏览器内核区别

1、IE 浏览器内核：Trident 内核，也是俗称的 IE 内核；
2、Chrome 浏览器内核：统称为 Chromium 内核或 Chrome 内核，以前是 Webkit 内核，现在是 Blink 内核；
3、Firefox 浏览器内核：Gecko 内核，俗称 Firefox 内核；
4、Safari 浏览器内核：Webkit 内核；
5、Opera 浏览器内核：最初是自己的 Presto 内核，后来是 Webkit，现在是 Blink 内核；
6、Edge 浏览器：webkit 内核

## HTML 语义化的理解

让页面内容结构化，便于浏览器搜索引擎解析
便于阅读和维护

## 多个标签页之间通信

vue 事件总线，webSocket，本地储存

## 浏览器 hack 技巧

Chorme 下 小于 12px 的文本按照 12px 显示，text-size-adjust:none

## 为什么初始化 css 样式

不同浏览器默认值不同

## css 优化、性能提升

Css 压缩，避免使用通配符规则，尽量使用类选择器代替标签选择器，避免对继承属性重复定义；慎用浮动、定位；去除空规则；样式抽离；

## 引用数据类型

原始数据类型直接存储在栈(stack)中的简单数据段，占据空间小、大小固定，属于被频繁使用数据，所以放入栈中存储；
引用数据类型存储在堆(heap)中的对象,占据空间大、大小不固定,如果存储在栈中，将会影响程序运行的性能；引用数据类型在栈中存储了指针，该指针指向堆中该实体的起始地址。当解释器寻找引用值时，会首先检索其在栈中的地址，取得地址后从堆中获得实体

## 什么是闭包（closure），为什么要用它？

闭包是指有权访问另一个函数作用域中变量的函数，创建闭包的最常见的方式就是在一个函数内创建另一个函数，通过另一个函数访问这个函数的局部变量,利用闭包可以突破作用链域，将函数内部的变量和方法传递到外部。闭包的特性： 1.函数内再嵌套函数 2.内部函数可以引用外层的参数和变量 3.参数和变量不会被垃圾回收机制回收

## 闭包的作用

最大用处有两个，一个是可以读取函数内部的变量，另一个就是让这些变量的值始终保持在内存中，不会在函数调用后被自动清除。

## 移动端适配

1、使用合理的 flex 布局 + 媒体查询做微调；
2、sass 函数 计算 1920 * 1080 下对应比例的 vw vh；$px / 1920 *100vh
3、<meta name="viewport" content="width=1920px, initial-scale=0.21" > （400/1920 = 0.21）
js 是单线程语言，宿主环境的多线程使它具有了异步的属性，浏览器才是真正实现异步的。

## 事件循环机制

同步的从上到下按顺序打印，异步的再执行。js 不断从任务队列里提取任务到主线程执行，事件队列也就是事件循环
异步宏任务先执行 然后在执行异步微任务。

```js script
setTimeout(() => {
  console.log(0);
});
new Promise((resolve) => {
  console.log(1);
  setTimeout(() => {
    resolve();
    var p1 = new Promise((n1, n2) => {
      n1(20);
    });
    p1.then(() => console.log(2));
    console.log(3);
    setTimeout(() => {
      console.log(9);
    }, 0);
  });
  new Promise((n1, n2) => {
    n1(20);
  }).then(() => console.log(4));
}).then(() => {
  console.log(5);
  var p2 = new Promise((n1, n2) => {
    n1(20);
  });
  p2.then(() => console.log(8));
  setTimeout(() => console.log(6));
});
console.log(7);

// 1，7，4，0，3，5，2，8，9，6
```

## Node 与浏览器的 Event Loop 差异

浏览器环境下，microtask 的任务队列是每个 macrotask 执行完之后执行。而在 Node.js 中，microtask 会在事件循环的各个阶段之间执行，也就是一个阶段执行完毕，就会去执行 microtask 队列的任务。
![avatar](https://gitee.com/HenrikChung/imgStore/raw/master/node&browser.png)
