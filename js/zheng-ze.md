### 示例
```
var isNumber = /^[0-9]+(\.[0-9]*)?$/g;
isNumber.test('123')   //true
isNumber.test('123')   //false
isNumber.exec('123')  // 返回被匹配到的值的数组
```

### test() & exec()
* test()返回true/false
* exec()返回匹配到的值的数组
* 如果正则表达式设置了全局标志，test() 的执行会改变正则表达式   lastIndex属性。连续的执行test()方法，后续的执行将会从 lastIndex 处开始匹配字符串，(exec() 同样改变正则本身的 lastIndex属性值).

### 截取字符串
* String.match(/.../)

### 常用
* 获取html页面名称：/\/(\w+\-*\w*\-*\w*)\.html/.exec(href)
```
function getPageName (url) {
    url=url||window.location.href;
    var pageName=/\/(\w+\-*\w*\-*\w*)\.html/.exec(url);
    return pageName!==null?pageName[pageName.length-1]:null
}
```

* 数字，最后2位不为00:`/^\d*[1-9]+(?!00)+.?$/`
* 数字‘-’分割获取父节点：`^(\d+(-\d+)*)(-\d+){1}$`


