### 子元素margin表现在父元素外层
#### 原因
外距合并：所有毗邻的两个或更多盒元素的margin将会合并为一个margin共享之。

毗邻的定义为：同级或者嵌套的盒元素，并且它们之间没有非空内容、Padding或Border分隔。

##### 解决方法
* 父级或子元素使用浮动或者绝对定位absolute，浮动或绝对定位不参与margin的折叠
* 父级overflow:hidden
* 父级设置padding（破坏非空白的折叠条件）
* 父级设置border