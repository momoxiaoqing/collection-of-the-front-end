### 箭头函数

#### 语法
void关键字：函数体只有一条语句并且不需要返回值，如：
```
let fun = () => void doesNotReturn();
```

#### 与普通函数的区别
1. 更简短
2. 本身没有this​​​​​​​，没有 prototype (原型)
3. 不绑定this，即：和函数外作用域一致，之后也不会改变
4. call | apply | bind 无法改变箭头函数中this的指向
5. 箭头函数不能作为构造函数使用
6. 不绑定arguments，取而代之用rest参数...代替arguments对象，来访问箭头函数的参数列表：箭头函数没有自己的arguments对象。在箭头函数中访问arguments实际上获得的是外层局部（函数）执行环境中的值。
7. 箭头函数不能用作Generator函数，不能使用yield关键字

不绑定arguments:
```js
// 普通函数
function A(a){
  console.log(arguments);
}
A(1,2,3,4,5,8);  //  [1, 2, 3, 4, 5, 8, callee: ƒ, Symbol(Symbol.iterator): ƒ]

// 箭头函数
let B = (b)=>{
  console.log(arguments);
}
B(2,92,32,32);   // Uncaught ReferenceError: arguments is not defined

// rest参数...
let C = (...c) => {
  console.log(c);
}
C(3,82,32,11323);  // [3, 82, 32, 11323]
```

#### 严格模式下依旧和函数外作用域一致

1、严格模式下，函数内访问不到全局this
```
    this.a = 1

    function add () {
        this.a++
        console.log(this.a)
    }
    add()  // 2

    function add2 () {
        'use strict'
        this.a++
        console.log(this.a)
    }
    add2() // Cannot read property 'a' of undefined


```

2、严格模式下依旧和函数外作用域一致
```
    this.a = 1

    'use strict' // 若不是严格模式，结果也是一样
    var add3=()=>{
        this.a++;
        console.log(this.a) //2
    }
    add3()
```

3、在promise函数体内，非严格模式下普通函数也可以访问外部this，但严格模式下不行，只有箭头函数可以访问
```
    this.a=1;
    Promise.resolve().then(() => console.log(this.a)); //2
    Promise.resolve().then(function() {console.log(this.a)});  //2

    'use strict'
    Promise.resolve().then(function() {console.log(this.a)});  // Cannot read property 'a' of undefined
```

注：ES6默认严格模式