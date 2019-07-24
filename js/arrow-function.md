## 箭头函数
### 作用
* 更简短
* 不绑定this，即：和函数外作用域一致

### 严格模式下依旧和函数外作用域一致

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