### 防止js重复提交
* setTimeout + clearTimeout（节流函数）
* 设定flag/js加锁
* 加减disabled
* 添加浮层比如loading图层防止多次点击

### 节流 throttle 


### 防抖 debounce
把多个信号合并为一个信号，利用setTimeout;

应用场合：input输入的格式验证、提交按钮的点击事件

```
<input type="text">
<script>
    function debounce(func, delay) {
        var timeout;
        return function(e) {
            console.log("清除",timeout,e.target.value)
            clearTimeout(timeout);

            var context = this, args = arguments
            console.log("新的",timeout, e.target.value)
            timeout = setTimeout(function(){

                //停止输入后执行的操作
                console.log("----")
                // func.apply(context, args);
                func(e);
            },delay)
        };
    }

    var validate = debounce(function(e) {
        console.log("change", e.target.value, new Date-0)
    }, 380);

    // 绑定监听
    document.querySelector("input").addEventListener('input', validate);
</script>
```


### 节流 throttle
应用场景：适用于动画场景，在比input, keyup更频繁触发的事件中，如resize, touchmove, mousemove, scroll

```
```

### debounce 和 throttle 的差异:
debounce：只执行一次，适用input输入的格式验证、提交按钮的点击事件

throttle：多长时间内必须执行一次，函数以一个频率重复执行，适用动画场景。

![](/assets/thottle.png)