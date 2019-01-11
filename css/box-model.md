### 盒子模型

#### 1、W3C标准盒模型 VS 怪异盒模型（IE 盒模型）
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
W3C标准盒模型（Chrome、IE9及以上）显示：

![](/assets/box.png)

怪异盒模型（IE 盒模型、IE8及以下）：

![](/assets/box-ie.png)

#### 2、box-sizing设置盒子模型
```
content-box // 怪异盒模型  total width: 100+(10+10)*2=140px
border-box //  W3C标准盒模型 total width:100px
```


#### 3、jquery的width() VS css('width',**)方法

* 在 box-sizing: border-box;下：

  width()指向content宽度；

  css('width',**)指向 content + padding + border
* 上一条和浏览器兼容性无关，IE9和IE6一致

height同理

