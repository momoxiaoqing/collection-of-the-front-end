#### 数据类型
8种数据类型：
* Boolean
* Null
* Undefined
* Number
* BigInt
* String
* Symbol ：唯一标识符，创建匿名的对象属性
* Object

未定义的值和定义未赋值的为 undefined，null 是一种特殊的 object，NaN 是一种特殊的 number。

#### cookies，sessionStorage 和 localStorage 的区别
共同点：都是保存在浏览器端，且同源的。

区别：

* cookie 数据始终在同源的 http 请求中携带（即使不需要），即 cookie 在浏览器和服务器间来回传递。
* 而 sessionStorage 和 localStorage 不会自动把数据发给服务器，仅在本地保存。
* cookie 数据还有路径（path）的概念，可以限制 cookie 只属于某个路径下。
*　存储大小限制也不同，cookie 数据不能超过 4k，同时因为每次 http 请求都会携带 cookie，所以 cookie 只适合保存很小的数据，如会话标识。
* sessionStorage 和 localStorage 虽然也有存储大小的限制，但比 cookie 大得多，可以达到 5M 或更大。
* 数据有效期不同，sessionStorage：仅在当前浏览器窗口关闭前有效，自然也就不可能持久保持；localStorage：始终有效，窗口或浏览器关闭也一直保存，因此用作持久数据；cookie 只在设置的 cookie 过期时间之前一直有效，即使窗口或浏览器关闭。
* 作用域不同，sessionStorage 在不同的浏览器窗口中不共享，即使是同一个页面；cookie 和 localStorage 在所有同源窗口中都是共享的。


#### document.write 和 innerHTML 的区别
* document.write 是直接写入到页面的内容流，如果在写之前没有调用 document.open, 浏览器会自动调用 open。每次写完关闭之后重新调用该函数，会导致页面被重写。
* innerHTML 则是 DOM 页面元素的一个属性，代表该元素的 html 内容。你可以精确到某一个具体的元素来进行更改。如果想修改 document 的内容，则需要修改 document.documentElement.innerElement。
* innerHTML 将内容写入某个 DOM 节点，不会导致页面全部重绘。
* innerHTML 很多情况下都优于 document.write，其原因在于其允许更精确的控制要刷新页面的那一个部分。
* document.write 是重写整个 document, 写入内容是字符串的 html；innerHTML 是 HTMLElement 的属性，是一个元素的内部 html 内容

#### new 操作符具体干了什么呢 ?
* 创建一个空对象，并且 this 变量引用该对象，同时还继承了该函数的原型。
* 属性和方法被加入到 this 引用的对象中。
* 新创建的对象由 this 所引用，并且最后隐式的返回 this 。

#### 重排&重汇


#### 强制缓存和协商缓存
强缓存：浏览器直接从本地（先内存后硬盘）读取文件  
header参数：
* Expires：过期时间，如果设置了时间，则浏览器会在设置的时间内直接读取缓存，不再请求
* Cache-Control：缓存设置
    *  max-age：用来设置资源（representations）可以被缓存多长时间，单位为秒；
    *  s-maxage：和max-age是一样的，不过它只针对代理服务器缓存而言；
    * public：指示响应可被任何缓存区缓存；
    * private：只能针对个人用户，而不能被代理服务器缓存；
    * no-cache：强制客户端直接向服务器发送请求，向服务器评估缓存响应的有效性。若资源变更，返回新内容，否则返回304。
    * no-store：禁止一切缓存（这个才是响应不被缓存的意思）。

协商缓存：浏览器从服务器读取文件  
Last-Modifed/If-Modified-Since和Etag/If-None-Match是分别成对出现的
* Etag/If-None-Match
    * Etag:Etag是属于HTTP 1.1属性，它是由服务器（Apache或者其他工具）生成返回给前端，用来帮助服务器控制Web端的缓存验证。
           Apache中，ETag的值，默认是对文件的索引节（INode），大小（Size）和最后修改时间（MTime）进行Hash后得到的
    * If-None-Match:当资源过期时，浏览器发现响应头里有Etag,则再次像服务器请求时带上请求头if-none-match(值是Etag的值)。服务器收到请求进行比对，决定返回200或304
* Last-Modifed/If-Modified-Since
    * Last-Modified：浏览器向服务器发送资源最后的修改时间
    * If-Modified-Since：当资源过期时（浏览器判断Cache-Control标识的max-age过期），发现响应头具有Last-Modified声明，则再次向服务器请求时带上头if-modified-since，表示请求时间。服务器收到请求后发现有if-modified-since则与被请求资源的最后修改时间进行对比（Last-Modified）,若最后修改时间较新（大），说明资源又被改过，则返回最新资源，HTTP 200 OK;若最后修改时间较旧（小），说明资源无新修改，响应HTTP 304 走缓存。
                       

#### 有哪些性能优化的方法 ？
1、内容优化
* 减少 HTTP 请求数。这条策略是最重要最有效的，因为一个完整的请求要经过 DNS 寻址，与服务器建立连接，发送数据，等待服务器响应，接收数据这样一个消耗时间成本和资源成本的复杂的过程。常见方法：合并多个 CSS 文件和 js 文件，利用 CSS Sprites 整合图像，Inline Images (使用 data：URL scheme 在实际的页面嵌入图像数据 )，合理设置 HTTP 缓存等。
* 减少 DNS 查找
* 避免重定向
* 使用 Ajax 缓存
* 延迟加载组件，预加载组件
* 减少 DOM 元素数量。页面中存在大量 DOM 元素，会导致 javascript 遍历 DOM 的效率变慢。
* 最小化 iframe 的数量。iframes 提供了一个简单的方式把一个网站的内容嵌入到另一个网站中。但其创建速度比其他包括 JavaScript 和 CSS 的 DOM 元素的创建慢了 1-2 个数量级。
* 避免 404。HTTP 请求时间消耗是很大的，因此使用 HTTP 请求来获得一个没有用处的响应（例如 404 没有找到页面）是完全没有必要的，它只会降低用户体验而不会有一点好处。

2、服务器优化
* 使用内容分发网络（CDN）。把网站内容分散到多个、处于不同地域位置的服务器上可以加快下载速度。
* GZIP 压缩
* 设置 ETag：ETags（Entity tags，实体标签）是 web 服务器和浏览器用于判断浏览器缓存中的内容和服务器中的原始内容是否匹配的一种机制。
* 提前刷新缓冲区
* 对 Ajax 请求使用 GET 方法
* 避免空的图像 src

3、 Cookie 优化
* 减小 Cookie 大小
* 针对 Web 组件使用域名无关的 Cookie

4、CSS 优化
* 将 CSS 代码放在 HTML 页面的顶部
* 避免使用 CSS 表达式
* 使用 < link> 来代替 @import
* 避免使用 Filters
  
5、javascript 优化
* 将 JavaScript 脚本放在页面的底部。
* 将 JavaScript 和 CSS 作为外部文件来引用。在实际应用中使用外部文件可以提高页面速度，因为 JavaScript 和 CSS 文件都能在浏览器中产生缓存。
* 缩小 JavaScript 和 CSS
* 删除重复的脚本
* 最小化 DOM 的访问。使用 JavaScript 访问 DOM 元素比较慢。
* 开发智能的事件处理程序
* javascript 代码注意：谨慎使用 with，避免使用 eval Function 函数，减少作用域链查找。
  
6、图像优化
* 优化图片大小
* 通过 CSS Sprites 优化图片
* 不要在 HTML 中使用缩放图片
* favicon.ico 要小而且可缓存

es6相关
---------
* [箭头函数与普通函数的区别](../js/es6/arrow-function.md)

####  for of & for in的区别
* for in是遍历（object）键名，for of是遍历（array）键值
* for...of是ES6新引入的特性,ie不支持
* for...of不能循环object，需要通过和Object.keys()搭配使用
```js
for(var key of Object.keys(student)){
    //使用Object.keys()方法获取对象key的数组
    console.log(key+": "+student[key]);
}
```

#### ES5 的继承和 ES6 的继承有什么区别 ？
 ES5 的继承时通过 prototype 或构造函数机制来实现。
* ES5 的继承实质上是先创建子类的实例对象，然后再将父类的方法添加到 this 上（Parent.apply(this)）。
* ES6 的继承机制完全不同，实质上是先创建父类的实例对象 this（所以必须先调用父类的 super()方法），然后再用子类的构造函数修改 this。

具体的：ES6 通过 class 关键字定义类，里面有构造方法，类之间通过 extends 关键字实现继承。子类必须在 constructor 方法中调用 super 方法，否则新建实例报错。因为子类没有自己的 this 对象，而是继承了父类的 this 对象，然后对其进行加工。如果不调用 super 方法，子类得不到 this 对象。

ps：super 关键字指代父类的实例，即父类的 this 对象。在子类构造函数中，调用 super 后，才可使用 this 关键字，否则报错。

#### 经典题
* JS 是单线程，你了解其运行机制吗 ？[参考](../js/jsyun-xing-ji-zhi.md)
* 7 分钟理解 JS 的节流、防抖及使用场景[5]
* JavaScript 常见的六种继承方式[6]
* 九种跨域方式实现原理（完整版）[7]
* 常见六大 Web 安全攻防解析[8]
* 一文读懂 HTTP/2 及 HTTP/3 特性[9]
* 深入理解 HTTPS 工作原理
* JavaScript 中的垃圾回收和内存泄漏[10]
* 你不知道的浏览器页面渲染机制[11]
* JavaScript 设计模式[12]
* 深入 javascript——构造函数和原型对象[13]

#### common.js/es6模块化方案的不同？







