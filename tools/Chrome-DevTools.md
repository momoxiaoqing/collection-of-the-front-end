### Chrome DevTools 调试技巧
[原文](https://mp.weixin.qq.com/s?__biz=MzI1ODk2Mjk0Nw==&mid=2247484952&idx=1&sn=a6dc94b9d15b05d724f15948884c0914&chksm=ea016574dd76ec62e4e6a70941cb574dc2ad6ac1ee03b6eab77a933353da9348011b4869abac&mpshare=1&scene=1&srcid=&sharer_sharetime=1579166625161&sharer_shareid=97b5de56c040c8b20d5d172683943dcf#rd)

* 控制台中直接访问页面元素： DOM选中元素，控制台输入$0，若页面含jquery，可$($0)获取对象

   控制台会存储最近 5 个被选择的元素和对象。当你在元素面板选择一个元素或在分析器面板选择一个对象,记录都会存储在栈中。可以使用 $x来操作历史栈,x 是从 0 开始计数的,所以 $0 表示最近选择的元素, $4 表示最后选择的元素。
* $_  //获取最近的控制台结果：
* $();  $$('div') //所有div ;  $x('html/body/div') //所有满足路径的元素
* console.table
* console.dir(object)/dir(object) // 获取参数所有的对象属性
* copy(any) //复制到剪贴板
* keys(object)/values(object) // 获取对象键值
* monitor(function)/unmonitor(function)  // 当调用指定的函数时,会将一条消息记录到控制台,该消息指示调用时传递给该函数的函数名和参数。
* monitorEvents(object[, events])/unmonitorEvents(object[, events])
* console.profile() //分析程序性能，若无，则打开main tools
```
console.profile('test')
func() //方法
console.profileEnd()
```
* clear()
* 截图：快捷键 ctrl+shift+p ,打开 Command Menu,输入 screenshot
* await + fetch //
 ```
 var res=await fetch(f)//f为在network中复制的fetch
 console.log(await res.json())
 ```
