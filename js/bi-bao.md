### 闭包
闭包是一个能够访问其他函数作用域的函数。

### 特性
* 基于词法作用域的查找规则
* 在一个函数内部定义一个内部函数，然后将内部函数作为值返回(函数当作值传递)，或者直接或间接的立即执行内部函数
* 拥有更长的生名周期，保持对当前词法作用域的引用

### 典型情况
1、将内部函数作为值返回

```
    function constfunc (v) {
        return function () {
            return v
        }
    }

    var func=[];
    for(var i=0;i<10;i++){
        func[i]=constfunc(i)
    }
    func[5]();    //5
```

```
    function outer () {
        var local=2;
        function inner () {
            return local+=2;
        }
        return inner
    }

    var fn=outer()
    console.log(fn())    //4
    console.log(fn())    //6

    var fn2=outer()
    console.log(fn2())    //4

/*------------------------------------变化后--------------------------------------*/
    function outer () {
        var local=2;
        function inner () {
            return local+=2;
        }
        return inner()
    }

    var fn=outer()
    console.log(fn)   //4
    console.log(fn)   //4

    var fn2=outer()
    console.log(fn2)  //4
```

2、直接或间接的立即执行内部函数
```
var local='global'
 function outer () {
     var local='local';
     function print () {
         console.log(local)
     }
     print();
 }

 outer(); // local
```


### 经典例子

```
    //将内部函数作为值返回
    function  print(index) {
        return setTimeout(function () {
            console.log(index)
            return index;
        }, 1000)
    }

    //直接或间接的立即执行内部函数
    function  print2(index) {
        setTimeout(function () {
            console.log(index)
        }, 1000)
    }


    for (var i = 0; i < 10; i++) {
       /* (function (e) {
            setTimeout(function () {
                console.log(e);
            },3000)
        })(i) */  // 和print2(i)同意义 打印0-9
        print(i)   //打印0-9
    }
```