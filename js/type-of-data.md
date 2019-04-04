### 7种数据类型
* 原始类型
  ```
   null
   undefined
   Boolean
   Number
   String
   Symbol
  ```
 * 对象类型 Object


### 注意
* 全局变量NaN（非数字值），和任何值都不相等，包括自身
   ```
   NaN === NaN //false
   NaN == NaN //false
   ```
* typeOf只能区别String、Number、Boolean、undefined
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

### 对象
#### 属性查询和设置
通过.或者[]来访问，其中[]中的表达式必须返回字符串或者返回一个可以转换成字符串的值(调用Object.toString())
```
[1,2,3].toString()  // "1,2,3"
({}).toString()     // "[object Object]"
(true).toString()   //"true"
(undefined).toString()  // Cannot read property 'tostring' of undefined
(null).toString()  // Cannot read property 'tostring' of null
```
例子：
```
 var a = {}
 var b = {a: 1, b: 2}
 var c = {a: 2, b: 3}
 var d = 1
 var e = 2
 var f = [1, 2, 3]
 var g = [1, 2, 3]
 a[b] = 1
 a[c] = 2
 a[d] = 3
 a[e] = 4
 a[f] = 5
 a[g] = 6
 console.log(a)
 /* {
      '1': 3,
      '1,2,3': 6,
      '2': 4,
      '[object Object]': 2
     }*/
```

#### Object.create() & 原型链 & 继承
Object.create(proto, [propertiesObject]):创建新对象

proto：新创建对象的原型对象，只能是Object或者null

propertiesObject：添加到新创建对象的可枚举属性（即其自身定义的属性)

对象的原型属性形成了原型链，从而实现属性的继承

注意：
* 属性赋值首先检查原型链，判断是否可赋值，若只读则不能赋值
* 赋值不改变原型链对象

#### delete
* delete只是断开属性和宿主对象的联系，不会去改变属性中的属性(可能引起内存泄露)
  ```
    var a = {
        p: {
            x: 1
        }
    }
    var b = a.p;

    delete a.p;
    console.log(b.x) //1
  ```

* delete只能删除自有属性，不能删除继承属性（要删除继承属性必须要从原型对象上删除它，这会影响到所有继承此原型的对象）
  ```
       var a = {
           p: 1
       }
       c = Object.create(a)
       d = Object.create(a)

       delete c.p;
       console.log(a.p) //1
       console.log(c.p) //1
       console.log(d.p) //1

       d = Object.create(a)
       delete a.p;
       console.log(a.p) //undefined
       console.log(c.p) //undefined
       console.log(d.p) //undefined
  ```

* delete不能删除可配置性为false的属性，比如内置对象、通过变量声明和函数声明创建的全局对象
 ```
       var a=1
       delete a   //false
       function fn () {}
       delete fn //false

       b=2  //this.b=2
       delete b   //true
 ```
* 任何用let或const声明的属性不能够从它被声明的作用域中删除。
* 严格模式下，删除不可配置属性或者省略对全局对象的引用，会报错；非严格模式下，返回false
 ```
      //严格模式下
      delete x //error
      delete this.x //true
 ```
* 删除数组元素，数组长度不变

#### 检测属性
* !==undefined
* in // 'x' in o; 可以区分不存在的属性和存在但值为undefined的属性
* hasOwnProperty()  //自有属性，继承的属性/方法都返回false
* propertyIsEnumerable()  //自有属性+可枚举性

#### 遍历
* for in //遍历可枚举的属性
* Object.keys() //返回key的数组
```
  Object.keys(obj).forEach(function (key) {
      console.log("obj ", key, ": ", obj[key]);
  });
```

##### for...in && for...of && forEach区别：

for...in ：设计用来遍历对象，也可遍历数组，但不建议，因为不按次序访问元素，以原始插入顺序迭代对象的可枚举属性。

for...of ：ES6中引入，IE不支持，遍历可迭代对象定义的迭代值。

for each of ：是E4X(ECMAScript for XML)的一部分，被禁用，可用for...in代替

forEach()：ES5，IE9+，对数组的每个元素执行一次提供的函数，遍历的范围在第一次调用 callback 前就会确定； 没有办法中止或者跳出 forEach() 循环，除了抛出一个异常
```js
   arr.forEach(callback[, thisArg]);
   // callback=function(){currentValue[,index,array]}
   // currentValue:数组中正在处理的当前元素
   // index:数组中正在处理的索引
   // array:正在操作的数组
```


for...in && for...of区别：
```js
   Object.prototype.objCustom = function() {};

   Array.prototype.arrCustom = function() {};

   let iterable = [3, 5, 7];
   iterable.foo = 'hello';

   for (let i in iterable) {
     console.log(i); // logs 0, 1, 2, "foo", "arrCustom", "objCustom"
   }

   for (let i in iterable) {
     if (iterable.hasOwnProperty(i)) {
       console.log(i); // logs 0, 1, 2, "foo"
     }
   }

   for (let i of iterable) {
     console.log(i); // logs 3, 5, 7
   }
```

#### JSON.stringify() && JSON.parse()
JSON.stringify():序列化

JSON.parse():还原

* JSON.stringify()支持：对象、数组、字符串、无穷大数字、true、false、null、RegExp、Error对象
* JSON.stringify()不支持：函数、undefined //不报错，返回结果undefined
* Infinity、-Infinity、null的序列化结果都为'null'
* RegExp、Error对象和{}的序列化结果为'{}'





