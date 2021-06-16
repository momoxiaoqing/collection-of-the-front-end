### js运行机制

#### GUI渲染线程
* 负责渲染浏览器界面，解析HTML，CSS，构建DOM树和RenderObject树，布局和绘制等
    * 解析html代码(HTML代码本质是字符串)转化为浏览器认识的节点，生成DOM树，也就是DOM Tree
    * 解析css，生成CSSOM(CSS规则树)
    * 把DOM Tree 和CSSOM结合，生成Rendering Tree(渲染树)
* 当我们修改了一些元素的颜色或者背景色，页面就会重绘(Repaint)
* 当我们修改元素的尺寸，页面就会回流(Reflow)
* 当页面需要Repaing和Reflow时GUI线程执行，绘制页面
* 回流(Reflow)比重绘(Repaint)的成本要高，我们要尽量避免Reflow和Repaint
* GUI渲染线程与JS引擎线程是互斥的
    * 当JS引擎执行时GUI线程会被挂起(相当于被冻结了)
    * GUI更新会被保存在一个队列中等到JS引擎空闲时立即被执行

#### JS引擎线程
* JS引擎线程就是JS内核，负责处理Javascript脚本程序(例如V8引擎)
* JS引擎线程负责解析Javascript脚本，运行代码
* JS引擎一直等待着任务队列中任务的到来，然后加以处理
    * 浏览器同时只能有一个JS引擎线程在运行JS程序，所以js是单线程运行的
    * 一个Tab页(renderer进程)中无论什么时候都只有一个JS线程在运行JS程序
* GUI渲染线程与JS引擎线程是互斥的，js引擎线程会阻塞GUI渲染线程
    * 就是我们常遇到的JS执行时间过长，造成页面的渲染不连贯，导致页面渲染加载阻塞(就是加载慢)
    * 例如浏览器渲染的时候遇到<script>标签，就会停止GUI的渲染，然后js引擎线程开始工作，执行里面的js代码，等js执行完毕，js引擎线程停止工作，GUI继续渲染下面的内容。所以如果js执行时间太长就会造成页面卡顿的情况

#### 宏任务
* 主代码块
* setTimeout
* setInterval
* setImmediate ()-Node
* requestAnimationFrame ()-浏览器

#### 微任务
* process.nextTick ()-Node
* Promise.then() //async/await类似
* catch
* finally
* Object.observe
* MutationObserver

#### Event Loop 流程
简略版：
![](/assets/js-brief.png)

详细版：
![](/assets/js.jpg)

注意：
1. 宏任务 -> 微任务 -> GUI渲染 -> [宏任务 -> ...]
2. 宏任务整体存入任务队列，不用马上拆分


###例子：
```js
function test() {
  console.log(1)
  setTimeout(function () { 	// timer1
    console.log(2)
  }, 1000)
}

test();

setTimeout(function () { 		// timer2
  console.log(3)
})

new Promise(function (resolve) {
  console.log(4)
  setTimeout(function () { 	// timer3
    console.log(5)
  }, 100)
  resolve()
}).then(function () {
  setTimeout(function () { 	// timer4
    console.log(6)
  }, 0)
  console.log(7)
})

console.log(8)

//1，4，8，7，3，6，5，2
```
```js
console.log('1');

setTimeout(function () {                   //timer1
    console.log('2');
    process.nextTick(function () {
        console.log('3');
    })
    new Promise(function (resolve) {
        console.log('4');
        resolve();
    }).then(function () {
        console.log('5')
    })
})
process.nextTick(function () {
    console.log('6');
})
new Promise(function (resolve) {
    console.log('7');
    resolve();
}).then(function () {
    console.log('8')
})

setTimeout(function () {                //timer2
    console.log('9');
    process.nextTick(function () {
        console.log('10');
    })
    new Promise(function (resolve) {
        console.log('11');
        resolve();
    }).then(function () {
        console.log('12')
    })
})

// 1 7 6 8 2 4  3 5 9 11 10 12
```



