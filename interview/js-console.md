### js 输出结果相关
1、以下输出结果是什么？
```javascript
var out = 25,
   inner = {
        out: 20,
        func: function () {
            var out = 30;
            return this.out;
        }
    };
console.log((inner.func, inner.func)());  // 25
console.log(inner.func());                // 20
console.log((inner.func)());              //20
console.log((inner.func = inner.func)()); //25
```
(inner.func, inner.func)和(inner.func = inner.func)返回的都是inner.func，是匿名函数，属于window，所以此时的this是window

考点：
* 作用域
* 运算符（赋值预算，逗号运算）

2、输出结果？
```javascript
if (!("a" in window)) {
    var a = 1;
}
alert(a);   // undefined
```
以上代码等价于
```javascript
var a;
if (!("a" in window)) {
    a = 1; // 变量提升
    console.log(1)
    alert(1)
}
alert(a);
```
因为：
* 所有的全局变量都是 window 的属性；`"变量名称" in window`可以用来检测全局变量是否声明
* 声明变量提升


3、
```javascript
var arr = [11,12,13,14,15];
for(var i = 0; i < arr.length; i++){
  arr[i] = function(){
    alert(i)
  }
}
arr[3]( "3"); //5
```
闭包

4、
```javascript
var x = 0;    　　
function test(){    　　　　
  alert(this.x);    　　
}    　　
var o = {};    　　
o.x = 1;    　　
o.m = test;    　　
o.m.apply(); // 0 
o.m.apply(o); // 1
```

5、js宏任务（macrotask）和微任务（microtask）
```javascript
setTimeout(function(){ console.log(4) }, 0);
new Promise(function(resolve){
    console.log(1)
    for( var i = 0 ; i <10000 ; i++ ){
        i == 9999 && resolve()
    }
    console.log(2)
}).then(function(){
    console.log(5)
});
console.log(3);
```
打印结果是12354，因为：

js里面有宏任务（macrotask）和微任务（microtask）。

因为 setTimeout 是属于 macrotask 的，而整个 script 也是属于一个 macrotask，promise.then 回调是 microtask，执行过程大概如下：

* 由于整个 script 也属于一个 macrotask，由于会先执行 macrotask 中的第一个任务，再加上 promise 构造函数因为是同步的，所以会先打印出 1 和 2；
* 然后继续同步执行末尾的 console.log(3) 打印出 3；
* 此时 setTimeout 被推进到 macrotask 队列中， promise.then 回调被推进到 microtask 队列中；
* 由于在第一步中已经执行完了第一个 macrotask ，所以接下来会顺序执行所有的 microtask，也就是 promise.then 的回调函数，从而打印出 5；
* microtask 队列中的任务已经执行完毕，继续执行剩下的 macrotask 队列中的任务，也就是 setTimeout，所以打印出 4。
