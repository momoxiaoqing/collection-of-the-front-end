### Chrome DevTools 调试技巧
[原文](https://mp.weixin.qq.com/s?__biz=MzI1ODk2Mjk0Nw==&mid=2247484952&idx=1&sn=a6dc94b9d15b05d724f15948884c0914&chksm=ea016574dd76ec62e4e6a70941cb574dc2ad6ac1ee03b6eab77a933353da9348011b4869abac&mpshare=1&scene=1&srcid=&sharer_sharetime=1579166625161&sharer_shareid=97b5de56c040c8b20d5d172683943dcf#rd)

* 控制台中直接访问页面元素： DOM选中元素，控制台输入$0，若页面含jquery，可$($0)获取对象

   控制台会存储最近 5 个被选择的元素和对象。当你在元素面板选择一个元素或在分析器面板选择一个对象,记录都会存储在栈中。可以使用 $x来操作历史栈,x 是从 0 开始计数的,所以 $0 表示最近选择的元素, $4 表示最后选择的元素。
* $_  //获取最近的控制台结果：
* $();  $$('div') //所有div ;  $x('html/body/div') //所有满足路径的元素
* id //必须为id="id"的DOM
* console.table(array)
* console.dir(object)/dir(object) // 获取参数所有的对象属性
* copy(any) //复制到剪贴板
* keys(object)/values(object) // 获取对象键值
* console.profile() //分析程序性能，若无，则打开main tools
```
console.profile('test')
func() //方法
console.profileEnd()
```
* clear() ////并没有清除变量&方法
* 截图：快捷键 ctrl+shift+p ,打开 Command Menu,输入 screenshot
* await + fetch //
 ```
 var res=await fetch(f)//f为在network中复制的fetch
 console.log(await res.json())
 ```


document.body.contentEditable = true; //编辑DOM内任何内容


#### 事件监听
1. getEventListeners(document.body)
```
 //useCapture默认为false:事件句柄在冒泡阶段执行;   true:事件句柄在捕获阶段执行
element.addEventListener(event,function,useCapture) 
element.removeEventListener(event,function,useCapture)
```

2. monitorEvents & unmonitorEvents
```js
monitorEvents(element,[eventName1,eventName2]) //element可用document.getElementById()或者document.querySelector
monitorEvents(document.getElementById("base"),'click');
unmonitorEvents(element)

```

3. Event.observe
```js
Event.observe(document.body, "click", function () {
    console.log("clicked");
});
```

```js
//error:
    getEventListeners($("#test"))
    getEventListeners($(".list2"))

//ok:
    getEventListeners(document.getElementById("test"))
   getEventListeners(document.querySelector('.list2'));
   getEventListeners(document.getElementById("test")).click[0].listener

document.querySelector('.list2').addEventListener("click", function onClick1() {
    console.log("click1");
}, true);
document.querySelector('.list3').addEventListener("click", function onClick2() {
    console.log("click2");
}, true);
document.querySelector('.list3').addEventListener("mousemove", function onMouseMove1() {
    console.log("mousemove");
}, true);
monitorEvents(document.getElementById("base"));
monitorEvents(document.querySelector("#base"));
monitorEvents(document.getElementById("base"),'click');
monitorEvents(document.getElementById("base"),['click','mouseover']);
```

#### 定时器
```js
console.time('mgTime')
var i;
for(i=0;;i++){
    if(i==10000){
        console.timeEnd('mgTime')
        break;
    }
}
```


