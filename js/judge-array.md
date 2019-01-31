### 判断是否数组方法

1、[instanceof](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/instanceof)
判断是否数组

 ```
 var arr = [];
 arr instanceof Array; // true

 var o = {};
 o instanceof Array; // false
 ```

2、原型链方法 [constructor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/constructor)

```
var ary = [1,23,4];
ary.__proto__.constructor==Array //true 和下行不同写法
ary.constructor==Array //true
ary.constructor==Object //false

var o={};
o.constructor==Object//true
o.constructor==Array  //false
```

3、[Object.prototype.toString()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString)

```
Object.prototype.toString.call([]) === '[object Array]' // true

//其他类型判断
Object.prototype.toString.call(123) === '[object Number]';
Object.prototype.toString.call('abc')) === '[object String]';
Object.prototype.toString.call(undefined) === '[object Undefined]';
Object.prototype.toString.call(true) === '[object Boolean]';
Object.prototype.toString.call(function(){}) === '[object Function]';
Object.prototype.toString.call(new RegExp()) === '[object RegExp]';
Object.prototype.toString.call(null) === '[object Null]';
```

4、[Array.isArray](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray)
```
Array.isArray([]) //true
```

### 各方法对比
* 兼容性：前三者都兼容，Array.isArray在IE9及以上才有效
* instanceof 和constructor 判断的变量，必须在当前页面声明

### [typeof](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof)
```
var a = 'abc'; console.log(typeof  a);//string
var b = 1; console.log(typeof b); //number
var c = false; console.log(typeof c); //boolean
console.log(typeof undefined); //undefined
console.log(typeof null); //object
console.log(typeof {});// object
console.log(typeof []);//object
console.log(typeof (function(){}));//function
```