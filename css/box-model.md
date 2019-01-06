### 盒子模型

1、
```
 <div class="content">content-model</div>
  .content{
             width: 100px;
             height: 100px;
             padding: 10px;
             background-color: #1b6d85;
             border: solid 10px #8a6d3b;
             margin: 10px;
         }
```
标准盒模型（Chrome、IE9）显示：
![](/assets/border-style.png)


2、jquery的width() VS css('width',**)方法

* width()指向content宽度；
  css('width',**)指向 content + padding + border
* 上一条和浏览器兼容性无关，IE9和IE6一致

height同理

