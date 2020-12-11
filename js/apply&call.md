### apply
this 指向第一个参数
```
var obj = {
    name : 'linxin'
}

function func(firstName, lastName){
    console.log(firstName + ' ' + this.name + ' ' + lastName);   //在浏览器中，this指向全局的 "window" 对象
}

func.apply(obj, ['A', 'B']);    // A linxin B
```

### call
```
var obj = {
    name: 'linxin'
}

function func(firstName, lastName) {
    console.log(firstName + ' ' + this.name + ' ' + lastName);
}

func.call(obj, 'C', 'D');       // C linxin D
```

### apply 和 call作用
* 改变 this 指向

* 借用别的对象的方法（实现继承）
```
var Person1  = function () {
    this.name = 'linxin';
}
var Person2 = function () {
    this.getname = function () {
        console.log(this.name);
    }
    Person1.call(this);
}
var person = new Person2();
person.getname();       // linxin
```

* 调用函数

apply、call 方法都会使函数立即执行

### apply & call & bind 区别
####  1、apply & call 区别：
方法传递的参数不同
```javascript
foo.call(this, arg1, arg2, arg3) == foo.apply(this, arguments) == this.foo(arg1, arg2, arg3);
```


在 EcmaScript5 中扩展了叫 bind 的方法，在低版本的 IE 中不兼容。它和 call 很相似，接受的参数有两部分，第一个参数是是作为函数上下文的对象，第二部分参数是个列表，可以接受多个参数。

call & bind 区别:
* bind 发返回值是函数

```
var obj = {
    name: 'linxin'
}

function func() {
    console.log(this.name);  // 在浏览器中，this指向全局的 "window" 对象
}

var func1 = func.bind(obj);     // undefined
func1();                        // linxin


var obj=func.call(obj);         // linxin

```
因为bind返回的是函数，所以不会和call一样立即执行。

* 参数的使用
```
function func(a, b, c) {
    console.log(a, b, c);
}
var func1 = func.bind(null,'linxin');

func('A', 'B', 'C');            // A B C
func1('A', 'B', 'C');           // linxin A B
func1('B', 'C');                // linxin B C
func.call(null, 'linxin');      // linxin undefined undefined
```

* 浏览器兼容性

IE9以后不支持bind

apply:ECMAScript 3rd Edition

call:ECMAScript 1st Edition

bind:EcmaScript5