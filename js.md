### 作用域问题：

1. setTimeOut\(\)中的$\(this\)指向Windows。



### 变量提升

JavaScript 仅提升声明，而不提升初始化



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

### 



