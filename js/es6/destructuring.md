### 解构赋值
按照一定模式，从数组、对象中提取值，对变量进行赋值

#### 注意事项：
* 若等号右边不是对象或数组，就先将其转为对象,undefined和null无法转为对象，会报错
* 允许指定默认值，只有当一个数组成员===undefined，默认值才会生效
* 默认值可以引用解构赋值的其他变量，但该变量必须已经声明
* 惰性求值：如果默认值是一个表达式，那么这个表达式是惰性求值的，即只有在用到的时候，才会求值
* 对象的属性没有次序，变量必须与属性同名，才能取到正确的值
* 对象的解构赋值真正被赋值的是后者
* 如果要将一个已经声明的变量用于解构赋值，必须非常小心
* 可以对数组进行对象属性的解构，因为数组本质是对象

#### 用途
1. 交换变量的值
2. 从函数返回多个值
3. 函数参数的定义
4. 提取 JSON 数据
5. 函数参数的默认值
6. 遍历 Map 结构
7. 输入模块的指定方法

#### 解构赋值& 圆括号
不能使用圆括号的情况：
* 变量声明语句
* 函数参数
* 赋值语句的模式(模式即json里的key)


[参考链接](https://es6.ruanyifeng.com/#docs/destructuring)

1、常见例子：
```
let [foo, [[bar], baz]] = [1, [[2], 3]];
foo // 1
bar // 2
baz // 3

let [ , , third] = ["foo", "bar", "baz"];
third // "baz"

let [head, ...tail] = [1, 2, 3, 4];
head // 1
tail // [2, 3, 4]

let [x, y, ...z] = ['a'];
x // "a"
y // undefined
z // []

//默认值
let [foo = true] = [];
foo // true
```

2、解析赋值 + Generator函数
```
function* fibs() {
  let a = 0;
  let b = 1;
  while (true) {
    yield a;
    [a, b] = [b, a + b];
  }
}

let [first, second, third, fourth, fifth, sixth] = fibs();  //[0,1,1,2,3,5]
sixth // 5
```

3、 对象的解构赋值真正被赋值的是后者
```
// 简写
let { foo,  bar } = { foo: 'aaa', bar: 'bbb' } 

// 等同于
let { foo: foo, bar: bar } = { foo: 'aaa', bar: 'bbb' };
```

```
let { foo: baz } = { foo: 'aaa', bar: 'bbb' };
baz // "aaa"
foo // error: foo is not defined
```
对象的解构赋值的内部机制，是先找到同名属性，然后再赋给对应的变量。真正被赋值的是后者，而不是前者


4、如果要将一个已经声明的变量用于解构赋值，必须非常小心
```
// 错误的写法
let x;
{x} = {x: 1};
// SyntaxError: syntax error

// 正确的写法
let x;
({x} = {x: 1});
```

5、对数组进行对象解构
```
let arr = [1, 2, 3];
let {0 : first, [arr.length - 1] : last} = arr;
first // 1
last // 3
```

6、数值和布尔值的解构赋值 
```
let {toString: s} = 123;
s === Number.prototype.toString // true

let {toString: s} = true;
s === Boolean.prototype.toString // true
```

7、函数参数解构
```
// 为变量x和y指定默认值
function move({x = 0, y = 0} = {}) {
  return [x, y];
}

move({x: 3, y: 8}); // [3, 8]
move({x: 3}); // [3, 0]
move({}); // [0, 0]
move(); // [0, 0]

// 为函数move的参数指定默认值
function move({x, y} = { x: 0, y: 0 }) {
  return [x, y];
}

move({x: 3, y: 8}); // [3, 8]
move({x: 3}); // [3, undefined]
move({}); // [undefined, undefined]
move(); // [0, 0]
```