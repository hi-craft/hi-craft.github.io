---
layout: post
title: 'Web知识点整理'
date: 2018-9-26
categories: 笔记
cover: 'https://farm5.staticflickr.com/4888/44117325450_67b0a8a0ce_k.jpg'
tags: note
---

# Interview

### CSS盒模型

分为标准盒模型和IE盒模型，标准盒模型width仅包括content部分，IE盒模型包括除Margin以外的部分。

切换盒模型可以借助CSS３的`box-sizing`属性

```css
box-sizing:content-box; // W3C 默认值
box-sizing:border-box; //IE
```

###  JS获取盒模型宽高

```javascript
dom.style.width/height  //只能获取内联样式的宽高，如所指定元素不存在内联样式，则无法获取
dom.currentStyle.width/height //仅限ie使用
window.getComputedStyle(dom).width/height //支持Firefox，Chrome
dom.getBoundingClientRect().width/height //返回元素的大小及其相对于视口的位置
```

## 块格式化上下文

#### BFC 定义

　　BFC(Block formatting context)直译为"块级格式化上下文"。它是一个独立的渲染区域，只有Block-level box参与， 它规定了内部的Block-level Box如何布局，并且与这个区域外部毫不相干。

#### BFC布局规则：

1. 内部的Box会在垂直方向，一个接一个地放置。
2. Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠
3. BFC的区域不会与float box重叠。
4. BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
5. 计算BFC的高度时，浮动元素也参与计算

下列方式会创建**块格式化上下文**

* 元素的 float 不是 `none`
* 元素的 position 为 `absolute` 或 `fixed`
* 元素的 display为 `inline-block` `table`
* overflow 值不为 `visible` 的块元素
* display为inline-block, table-cell, table-caption, flex, inline-flex

###　DOM

#### DOM事件级别

```javascript
DOM0 element.onclick = function(){}
DOM2 element.addEventListener("click",function(){},flase)
DOM2 element.addEventListener("keyup",function(){},flase)
```

#### DOM事件模型

**事件捕获和事件冒泡**

####　DOM事件流

**事件捕获＝>目标节点=>事件冒泡**

#### DOM事件捕获具体流程

**window=>document=>html**

获取html

````javascript
document.documentElemenet //文档的文档元素, 作为一个元素对象返回
````

#### EVENT对象的常见应用

```javascript
event.preventDefault() ; //阻止默认行为
event.cancelBubble(); //阻止默认行为 ,IE专用
event.stopPropagation() ; //阻止冒泡，阻止把事件分派到其他节点
event.stopImmediatePropagation(); //如果有多个相同类型事件的事件监听函数绑定到同一个元素，当该类型的事件触发时，它们会按照被添加的顺序执行。如果其中某个监听函数执行了当前方法，则当前元素剩下的监听函数将不会被执行。
e.target //指向触发事件监听的对象。
e.currentTarget //指向添加监听事件的对象。
```



#### 自定义事件

```javascript
let selfEvent = new Event('self',{
      "bubbles" : true,//可选，Boolean类型，默认值为 false，表示该事件是否冒泡。
      "cancelable" : false,//可选，Boolean类型，默认值为 false， 表示该事件能否被取消。
    });
let doc = document.querySelector('.layout .left');
doc.addEventListener('self', () => {
  alert('This is Self Event');
})
doc.dispatchEvent(selfEvent)
```

#### CustomEvent()

```javascript
var custom = new CustomEvent('custom',{
      "detail" : {  //可携带额外的数据
        age : 18
      },
      "bubbles" : true,
      "cancelable" : false,
    });
    用法与Event()相同，可携带数据，IE不支持
```

#### HTTP协议的主要特点

 * 简单快速  每个资源的URI是固定的，统一资源定位符，需要访问资源只需要输入URI

 * 灵活    每个HTTP协议会有头类型，通过一个HTTP协议就可以完成不同类型数据的传输

 * 无连接  每次连接后就会断开

 * 无状态  无法记住两次连接 连接者的身份，每次连接都是新的


#### HTTP协议

HTTP报文的组成部分

##### 请求报文

 * 请求行  包含HTTP方法，页面地址，HTTP协议以及版本
 * 请求头 一些key-value值告诉服务端需要什么内容，以什么类型返回
 * 空行 用以服务端区分请求头和请求体
 * 请求体 数据部分

##### 相应报文

* 状态行
* 响应头
* 空行
* 相应体

####  HTTP方法

* GET ———————>   获取资源
* POST ———————->  传输资源
* PUT ————————> 更新资源
* DELETE ———————-> 删除资源
* HEAD ————————–> 获得报文首部


#### GET和POST的区别

 * GET在浏览器回退是无害的，而POST会再次提交请求   记

* GET产生的URL地址可以被收藏，而POST不可以
* GET请求会被浏览器主动缓存，而POST不可以    记
* GET请求只能进行URL编码，而POST支持多种编码方式    
* GET请求参数会被完整保留在浏览器历史记录里，而POST中的参数不会被保留  记
* GET请求在URl中传送的参数是有长度限制的，而POST没有限制  记
* 对参数的数据类型，GET只接受ASCLL字符，而POST没有限制  
* GET比POST更不安全，因为参数直接暴露在URL上，所以不能用来传递敏感信息
* GET参数通过URL传递，POST放在Reauest body中   记

####　HTTP状态码

* 1xx : 提示信息－表示请求已接收，继续处理
* 2xx： 成功-表示请求已被成功接收
* 3xx：重定向-要完成请求必须进行更进一步的操作
* 4xx：客户端错误-请求有语法错误或请求无法实现
* 5xx：服务器错误-服务器未能实现合法的请求 
* 200 OK ： 客户端请求成功
* 206 Partial Content：客户发送了一个带有Range头的GET请求，服务器完成了它
* 403 Forbidden：对被请求页面的访问被禁止
* 404 Not Found： 请求资源不存在

#### HTTP持久连接

HTTP协议采用“请求-应答”模式，当使用普通模式，即非Keep-Alive模式时，每个请求/应答客户和服务器都要新建一个连接，完成之后立即断开连接（HTTP协议为无连接的协议）

当使用Keep-Alive模式（又称持久连接，连接重用）时，Keep-Alive功能使客户端到服务器端的连接持续有效，当出现对服务器的后继请求时，Keep-Alive功能避免了建立或者重新建立连接

Keep-Alive在HTTP1.1中存在

#### HTTP协议管线化(了解)

在使用持久连接的情况下，某个连接上消息的传递类似于

请求1->响应1->请求2->响应2->请求3->响应3

某个连接上的消息变成了类似这样

请求1->请求2->请求3->响应1->响应2->响应3

* 管线化机制通过持久连接完成，仅HTTP/1.1支持此技术 —记
* 只有GET和HEAD请求可以进行管线化，而POST则有所限制 —记
* 初次创建连接时不应启动管线机制，因为对方服务器不一定支持HTTP/1.1版本的协议  —记
* 管线化不会影响响应到来的顺序，如上面的例子所示，响应返回的顺序并未改变
* HTTP/1.1要求服务器端支持管线化，但并不要求服务器端也对响应进行管线化处理，只是要求对于管线化的请求不失败即可
* 由于上面提到的服务器端问题，开启管线化很可能并不会带来大幅度的性能提升，而且很多服务器端和代理程序对管线化的支持并不好，因此现代浏览器如Chrome和Firefox默认并未开启管线化支持

### 原型链

##### 创建对象的几种方法

```
//对象字面量

var o1 = {name:"o1"};        //{obj: 1}
var o2 = new Object({name:'o2'}); //{obj: 1}

//构造函数

var m = function(name){this.name = name;}
var o3 = new m('o3');  //m {name: "o3"}

//Obejct.create

var p = {name:'p'}
var o4 = Object.create(p);  //{ }
```

只有实例才有``__proto__``



 只有对象才有``prototype``

构造函数的``prototype``指向他的原型对象，原型对象含有一个``constructor``指针指向构造函数，实例有一个``__proto__``指向生成这个实例的构造函数的原型对象，实例还有一个``constructor`指针指向生成这个实例的构造函数

```javascript
m.prototype.constructor === o3.constructor //true
```

``instanceof``的原理是判断实例对象``__proto__``属性与构造函数的``prototype``属性是不是引用同一个地址

实例 ``instanceof``其原型链上任意一个构造函数都返回``true``

如果需要判断当前实例是由原型链上哪个构造函数生成的

```javascript
o3.__proto__.constructor === m //true
```

#### new 运算符

当运行new运算符后

* 一个新对象被创建，它继承自构造函数的原型对象
* 构造函数被执行，执行的时候，相应的传参会被传入，同时上下文（this）会被指定为这个新实例。
* 如果构造函数返回了一个“对象”，那么这个对象会取代整个new出来的的结果，如果构造函数没有返回对象，那么new出来的结果为步骤1创建的对象



**Object.create()**方法创建一个新对象，使用现有的对象来提供新创建的对象的``__proto__``。 

所以通过Object.create()方法创建的对象，如果没有添加第二个参数，就是一个空对象，创建时传入的对象成为了这个新的空对象的原型对象

### 面向对象

#####  继承

###### ES5 借助构造函数实现继承

```javascript
function Animal(){
    //do something
}
function Parent1(){
    this.name = 'parent1';
}
function Child1(){
  Parent1.call(this); //将父级构造函数的This指向子构造函数的实例
    this.type = 'child1';
}
```

##### 借助原型链实现继承

```javascript
function Parent(){
  this.name = 'parent';
    this.arr = [1,2,3]
}
function Child(){
  this.type = 'child';
}
Child.prototype = new Parent();

var o1 = new Child();
var o2 = new Child();
o1.arr.push(4) ;
o1.arr //[1,2,3,4]
o2.arr //[1,2,3,4]
```

将父类对象作为子类构造函数的原型对象，所以父类对象中所有的属性和方法在子类对象中均是共享的，也就是说，所有的子类对象共享一份父类对象的属性和方法

##### 构造函数与原型链组合继承

```javascript

        function Parent() {
            this.name = 'parent';
            this.arr = [1, 2, 3]
        }

        function Child() {
            Parent.call(this);
            this.type = 'child'
        }
        Child.prototype = new Parent();
        var o1 = new Child;
        var o2 = new Child;
        o1.arr.push(4)
        console.log(o1.arr,o2.arr) //[1,2,3,4],[1,2,3]
```

缺点

多次执行父类构造函数，子类与父类的原型对象是同一个，所以无法判断实例到底是哪个构造函数生成的实例，Child没有自己的constructor







```javascript
        function Parent() {
            this.name = 'parent';
            this.arr = [1, 2, 3]
        }

        function Child() {
            Parent.call(this);
            this.type = 'child'
        }
        Child.prototype = Parent.prototype;
        var o1 = new Child;
        var o2 = new Child;
        o1.arr.push(4)
        console.log(o1.arr,o2.arr) //[1,2,3,4],[1,2,3]
```

这种方式同样可以实现继承，因为在子类通过构造函数继承的时候，已经拿到了父类构造函数的所有属性和方法，剩下的只需要拿到父类构造函数原型链上的方法和属性，这样将子类构造函数的原型对象设置为父类构造函数的原型对象即可实现

缺点

子类与父类的原型对象是同一个，所以无法判断实例到底是哪个构造函数生成的实例

```javascript
function Parent() {
  this.name = 'parent';
  this.arr = [1, 2, 3]
}
function Child() {
  Parent.call(this);
  this.type = 'child'
}
Child.prototype = Object.create(Parent.prototype);
Child.prototype.constructor = Child;
```

这样在子类构造函数的原型对象与父类构造函数的原型对象构建了一个中间层，将其隔离的目的是为了手动设置子类构造函数的原型对象的constructor而不影响父类构造函数的原型对象的constructor，上面的第二种写法如果直接指定子类的构造函数的原型对象的constructor，那么父类的构造函数的原型对象的constructor也会被改变

###　通信

什么是同源策略及限制，前后端如何通信，如何创建Ajax，跨域通信的几种方式

1. 同源策略限制从一个源加载的文档或脚本如何与来自另一个源的资源进行交互。这是一个用于隔离潜在恶意文件的关键的安全机制。源包括协议，域名，端口

* Cookie，LocalStorage 和IndexDB无法获取

* DOM 无法获得

* Ajax无法发送

2. 前后端如何通信:Ajax,WebSocket(不受同源策略限制),CORS(支持跨域通信与同步通信)

3. 1

4. 跨域通信的几种方式: 

   * JSONP

   * HASH(URL后面连接的#叫做HASH,HASH的改变并不会刷新页面，URL后面连接的?叫做SEARCH,SEARCH的改变会触发页面刷新)
   * postMessage
   * WebSocket
   * CORS

 JSONP

```javascript
function addScriptTag(src) {
  var script = document.createElement('script');
  script.setAttribute("type","text/javascript");
  script.src = src;
  document.body.appendChild(script);
}
url:http://tcc.taobao.com/cc/json/mobile_tel_segment.htm?tel=18845798396&callback=cb
callback需要手动指定，且为全局函数，用于接收返回数据
```

HASH

利用hash，场景是当前页面A通过iframe或frame嵌入了跨域的页面B

```javascript
var src = originURL + '#' + data;
document.getElementById('myIFrame').src = src;
子窗口通过监听hashchange事件得到通知。
window.onhashchange = checkMessage;

function checkMessage() {
  var message = window.location.hash;
  // ...
}
同样的，子窗口也可以改变父窗口的片段标识符。
```

postMessage

```javascript
var popup = window.open('http://bbb.com', 'title');
popup.postMessage('Hello World!', 'http://bbb.com');
窗口A向窗口B发送信息
Bwindow.postMessage('data',"url");
在B窗口中监听
window.addEventListener('message',function(event){
    console.log(event.origin); //http:A.com
    console.log(event.source); //Awindow
    console.log(event.data); //data!
})
```



#### [WebSocket](http://www.ruanyifeng.com/blog/2017/05/websocket.html)

```javascript
var ws = new WebSocket("wss://echo.websocket.org");//ws非加密，wss加密
        var tet = document.querySelector('#text');

        ws.onopen = function(evt) {
            tet.innerHTML += `<br/>Connection open ...<br/>`
            ws.send("HEYYYYYY");
        };

        ws.onmessage = function(evt) {
            tet.innerHTML += `Received Message:${evt.data}<br/>`
            ws.close();
        };

        ws.onclose = function(evt) {
            tet.innerHTML += `Connection closed.`
        };

```

#### CORS

CORS是一个W3C标准，全称是"跨域资源共享"（Cross-origin resource sharing）。

它允许浏览器向跨源服务器，发出[`XMLHttpRequest`](http://www.ruanyifeng.com/blog/2012/09/xmlhttprequest_level_2.html)请求，从而克服了AJAX只能[同源](http://www.ruanyifeng.com/blog/2016/04/same-origin-policy.html)使用的限制。

CORS与JSONP的使用目的相同，但是比JSONP更强大。

JSONP只支持`GET`请求，CORS支持所有类型的HTTP请求。JSONP的优势在于支持老式浏览器，以及可以向不支持CORS的网站请求数据。

### 安全

#### CSRF

跨站请求伪造(Cross-site request forgery)缩写CSRF

![](https://farm5.staticflickr.com/4823/45021378645_a7d07320ba_o.png)

当用户注册并登录网站A后，网站A就会下放Cookie保存在浏览器中，用于下次登录。网站B会存在一个引诱链接，当用户点击后网站B会调用网站A的API接口，浏览器就会自动上传保存在浏览器中的Cookie，网站A通过验证后就会允许网站B的登录行为

#### 防御

* Token验证
  * Token是服务器自动存储在本地的一个令牌，只有在访问后同时发送了Cookie和Token后，服务器才会允许登录请求
* Referer验证
  * 服务器判断页面来源，如果页面来源为第三方网站则拦截请求
* 隐藏令牌
  * 类似Token，隐藏在HTTP请求头中

#### XSS

跨域脚本攻击(cross-site scripting)

[CLICK](http://www.imooc.com/learn/812)

通过合法的渠道向页面中注入js脚本

禁止执行用户插入的js脚本

CSRF利用网站的漏洞发起攻击，XSS则是通过直接注入js执行脚本，而且CSRF需要用户曾经发起过登录行为

### 算法

![](https://farm5.staticflickr.com/4832/30994826027_2c20d9a75e_o.png)

* 排序
  * [快速排序](https://segmentfault.com/a/1190000009426421)
  * [选择排序](https://segmentfault.com/a/1190000009366805)
  * [希尔排序](https://segmentfault.com/a/1190000009461832)
* [堆栈，队列，链表](https://juejin.im/entry/58759e79128fe1006b48cdfd)
* [递归](https://segmentfault.com/a/1190000009857470)
* 波兰式和逆波兰式
  * [理论](http://www.cnblogs.com/chenying99/p/3675876.html)
  * [源码](https://github.com/Tairraos/rpn.js/blob/master/rpn.js)

#### 渲染机制

* 什么是DOCTYPE及作用
  * DTD（document type definition，文档类型定义）是一系列的语法规则，用来定义XML或（X）HTML的文件类型。浏览器会使用它来判断文档类型，决定使用何种协议来解析，一起切换浏览器模式
  * DOCTYPE是用来声明文档类型和DTD规范的，一个主要的用途便是文件的合法性验证。如果文件代码不合法，那么浏览器解析时便会出现一些差错
  * HTML5``<!DOCTYPE hlml>``
  * HTML4.01Strict 该DTD包含所有HTML元素和属性,但不包括展示性和弃用的元素（比如font）
  * HTML4.01 Transitional 该DTD包含所有HTML元素和属性，包括展示性的和弃用的元素（比如font）
* 浏览器渲染过程
  * ![](https://farm5.staticflickr.com/4809/45021378445_ce1252d292_o.png)
  * HTML通过HTML Parse转成DOM Tree Style Sheets通过CSS Parse转成Style Rules，他们之间通过整合形成Render Tree，同时浏览器生成Layout布局，确定元素位置，然后浏览器开始绘制，显示
  * ![](https://farm5.staticflickr.com/4896/44117497750_c268c77261_o.png)
  * ![](https://farm5.staticflickr.com/4810/30994825677_1b19f57919_o.png)
  * ![](https://farm5.staticflickr.com/4869/30994825577_5322b90364_o.png)
  * ![](https://farm5.staticflickr.com/4914/45021378175_beee00ef93_o.png)
* 重排Reflow
  * 定义
    * dom结构中的各个元素都有自己的盒子（模型），这些都需要浏览器根据各种样式来计算并根据计算结果将元素放到它该出现的位置，这个过程称之为reflow
  * 触发Reflow
    * 当你增加，删除，修改DOM结点时，会导致Reflow或Repaint
    * 当你移动DOM的位置，或是搞个动画的时候
    * 当你修改CSS样式的时候
    * 当你Resize窗口的时候（移动端没有这个问题），或是滚动的时候
    * 当你修改网页的默认字体时
* 重绘Repaint
  * 定义
    * 当各种盒子的位置，大小以及其他属性，例如颜色，字体大小等都确定下来后，浏览器于是便把这些元素都按照各自的特性绘制了一遍，于是页面的内容出现了，这个过程称之为Repaint
  * 触发Repaint
    * DOM改动
    * CSS改动
* 布局Layout

 

#### JS运行机制

  JS单线程运行，也就是JS同时只能处理一个事件，SetTimeout得以通过异步的方式执行，是因为JS采用了任务队列的方式

```javascript
console.log(1);
setTimeout(()=>console.log(2),0);
console.log(3);

//1 3 2

console.log('A');
setTimeout(()=>console.log('B'),0);
while(true){}

//A
```

在上面的例子中，setTimeout属于异步队列。在所有的同步队列执行完毕之前，任何异步队列都不会被响应。

```javascript
for(var i=0;i<4;i++){
    setTimeout(function(){
        console.log(i);
    },1000);
};
for(var i=0;i<4;i++){
    setTimeout(function(){
        console.log(i);
    },0);
};
// 4 4 4 4
当JS解析遇到setTimeout函数时，就会将其视作异步任务，并通过Time模块将其接管，只要当同步任务执行完毕后，才会开始读取异步任务队列
```

#### 任务队列和Event Loop

![](https://farm5.staticflickr.com/4816/30994825287_806c199fa3_o.png)

Event Loop就是当同步任务队列读取后，开始读取异步任务队列，当全部执行完毕后，重新开始读取同步任务队列。

##### 异步任务

* setTimeout 和setInterval
* DOM事件
* ES6的Promise

#### 页面性能

1. 资源压缩合并，减少HTTP请求
2. 非核心代码异步加载=>异步加载的方式=>异步加载的区别
   1. 异步加载的方式
      1. 动态脚本加载
      2. defer（常用）
      3. async
   2. 异步加载的区别
      1. defer是在HTML解析完之后才会执行，如果是多个，按照加载的顺序依次执行
      2. async是在加载完之后立即执行，也就是和加载和渲染文档的过程并行执行，如果是多个，执行顺序和加载顺序无关
3. **利用浏览器缓存=>缓存的分类=>缓存的原理**
   1. 缓存的分类（以下为HTTP请求头内容）
      1. 强缓存(第一条是服务器返回的绝对时间，第二条是相对时间，当服务器时间与本地时间不一致时，以后者为准，当在3600s之内直接读取本地资源，不再与服务器通信)
         1. ``Expires Expires:Thu，21 Jan 2017 23:39:02 GMT``
         2. ``Cache-Control Cache-Control:max-age=3600``
      2. 协商缓存（第一条是上次响应请求的时间，Etag类似资源的HASH值，当需要请求服务器时，服务器会返回资源的Hash值，用以和本地的Etag对比，查看资源是否发生更新）
         1. ``Last-Modified If-Modified-Since Last-Modified:Web,26 Jan 2017 00:35:11 GMT Etag If-None-Match``
4. 使用CDN
5. 预解析DNS,页面中A标签默认打开DNS预解析，如果页面协议为``https``那么浏览器会默认关闭这个功能，第一句代码就是为了强制打开A标签的DNS预解析
   ``<meta http-equiv="x-dns-prefetch-control" content="on">``
   ``<link rel="dns-prefetch" href="//host_name_to_prefetchcom"``
#### 错误监控

* ##### 前端错误的分类

  * 即时运行错误：代码错误

  * 资源加载错误

* ##### 错误的捕获方式

  * 跨域的Js运行错误可以捕获吗，错误提示什么，应该怎么处理？
    * 可以捕获错误，但是无法取得具体信息，错误详情会显示为NULL
    * 解决方式
      * 在script标签中增加crossorigin属性
      * 设置JS资源响应头``Access-Control-Allow-Origin``
  * 即时运行错误的捕获方式
    * 1)try..catch 
    * 2)window.onerror（无法捕获资源加载错误）
  * 资源加载错误的捕获方式
    * 1)object.onerror 
    * 2)perfofmance.getEntries()（返回已经成功加载资源数组，可以通过比较需要加载的资源数组来得到那些资源没有被正确加载） 
    * 3)Error事件捕获，可以通过addEventListener的方式来绑定Error事件，并且设置为True（捕获方式接收事件）

* #####　上报错误的基本原理

  * 采用Ajax通信的方式上报

  * 利用Image对象上报（常用）

    ```javascript
    (new Image()).src="URL"
    ```

 