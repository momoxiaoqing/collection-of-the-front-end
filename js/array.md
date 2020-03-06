### Array

#### 常用方法：
* fill：IE不支持
* reduce：IE9+，累计值，但不改变原数组

定义数组长度及其值：
```
array = Array(5).fill(1);
```

求和：
```
  var a = [1, 2, 3, 4]
    var sum = a.reduce(function (accumulator, currentValue, currentInde, sourceArray) {
        return accumulator + currentValue
    })
    console.log(sum)
```

合并数组：
```
var a=[1,2]
var b=[3,3]
var c=[...a,...b] //[1, 2, 3, 3]
```


获取数组唯一值：
```
var c=[1, 2, 3, 3]
Array.from(new Set(c)) //[1, 2, 3]
```
[Aarray MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)

