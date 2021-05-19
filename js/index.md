#### js基础语法

### 声明提升
* JavaScript 仅提升声明，而不提升初始化
* 函数声明的优先级高于变量声明的优先级
* 函数声明的函数体也会被提升，但函数表达式不会

```
/* 函数声明式 */
(function(){
    fn();
    function fn() {
        console.log('来自函数声明式fn');
    }
})();

/* 函数表达式 */
(function(){
    fn();
    var fn = function() {
        console.log('来自函数表达式fn');
    }
})();
```

输出：

`来自函数声明式fn`

`fn is not a function`


#### 浅拷贝&深拷贝
* 浅拷贝：对象共用一个内存地址
* 深拷贝：将对象放到一个新的内存


