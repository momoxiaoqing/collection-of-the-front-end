### Generator 函数
可以理解成一个状态机，封装了多个内部状态  
[参考地址](https://es6.ruanyifeng.com/#docs/generator)

特征：
* function*
* yield //暂停执行的标记

#### 注意事项
* 调用 Generator 函数后，该函数并不执行，返回的也不是函数运行结果，而是一个指向内部状态的指针对象
* 每次调用next方法，内部指针就从函数头部或上一次停下来的地方开始执行，直到遇到下一个yield表达式（或return语句）为止
* yield表达式如果用在另一个表达式之中，必须放在圆括号里面
```
function* demo() {
  console.log('Hello' + yield); // SyntaxError
  console.log('Hello' + yield 123); // SyntaxError

  console.log('Hello' + (yield)); // OK
  console.log('Hello' + (yield 123)); // OK
}
```
* yield表达式用作函数参数或放在赋值表达式的右边，可以不加括号


#### yield * return
* 每次遇到yield，函数暂停执行，下一次再从该位置继续向后执行，而return语句不具备位置记忆的功能
* return 只能执行一次，yield可以多个

#### next()传参
yield表达式本身没有返回值，或者说总是返回undefined。next方法可以带一个参数，该参数就会被当作上一个yield表达式的返回值

#### 遍历
* for...of：一旦next方法的返回对象的done属性为true，循环就会中止，return 是不会遍历到的
* 扩展运算符（...）
* 解构赋值
* Array.from

```js
function* numbers () {
  yield 1
  yield 2
  return 3
  yield 4
}

// 扩展运算符
[...numbers()] // [1, 2]

// Array.from 方法
Array.from(numbers()) // [1, 2]

// 解构赋值
let [x, y] = numbers();
x // 1
y // 2

// for...of 循环
for (let n of numbers()) {
  console.log(n)
}
// 1
// 2
```

#### Generator.prototype.throw() 
* Generator 函数返回的遍历器对象，都有一个throw方法，可以在函数体外抛出错误，然后在 Generator 函数体内捕获
* throw方法抛出的错误要被内部捕获，前提是必须至少执行过一次next方法
* throw方法被捕获以后，会执行一次next方法，是try...catch后的语句
* 如果 Generator 函数内部没有部署try...catch代码块，那么throw方法抛出的错误，将被外部try...catch代码块捕获。
* Generator 函数体内抛出的错误，也可以被函数体外的catch捕获，一旦 Generator 执行过程中抛出错误，且没有被内部捕获，就不会再执行下去了

注意：全局的throw：catch语句块，捕获了抛出的a错误以后，就不会再继续try代码块里面剩余的语句了

#### Generator.prototype.return() 
返回给定的值，并且终结遍历 Generator 函数  
如果 Generator 函数内部有try...finally代码块，且正在执行try代码块，那么return()方法会导致立刻进入finally代码块，执行完以后，整个函数才会结束。

#### next() & throw() & return() 
作用都是让 Generator 函数恢复执行，并且使用不同的语句替换yield表达式  
* next()是将yield表达式替换成一个值
* throw()是将yield表达式替换成一个throw语句
* return()是将yield表达式替换成一个return语句

#### yield*
用来在一个 Generator 函数里面执行另一个 Generator 函数  
yield*后面的 Generator 函数（没有return语句时），等同于在 Generator 函数内部，部署一个for...of循环

```js
function* inner() {
  yield 'hello!';
}

function* outer1() {
  yield 'open';
  yield inner();
  yield 'close';
}

var gen = outer1()
gen.next().value // "open"
gen.next().value // 返回一个遍历器对象
gen.next().value // "close"

function* outer2() {
  yield 'open'
  yield* inner()
  yield 'close'
}

var gen2 = outer2()
gen2.next().value // "open"
gen2.next().value // "hello!"
gen2.next().value // "close"
```

#### Generator作为对象属性
```js
let obj = {
  * myGeneratorMethod() {
  }
};
```
等价于：
```js
let obj = {
  myGeneratorMethod: function* () {
    // ···
  }
};
```