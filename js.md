### 作用域问题：

1. setTimeOut\(\)中的$\(this\)指向Windows。

### 变量提升

* JavaScript 仅提升声明，而不提升初始化

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

### 点击事件触发两次\(冒泡事件\)

```
 <label class="radio " style="margin-left: 88px;">
            <input type="radio" value="3" name="orginType" class="notMove"> 非移动员工
 </label>
```

上述代码会引起click触发两次

解决方法：

```
$("label").click(function (e) {
         if ($(e.target).is("input"))
         return;
});
```

### 关于数组
Array方法：
* fill
* fill

[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)


