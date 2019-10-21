### vertical-align
只对行内元素、表格单元格元素有效

#### 行内元素取值
相对父元素：
* baseline: 默认值，使元素的基线与父元素的基线对齐，因浏览器而异
* sub: 使元素的基线与父元素的下标基线对齐
* super: 使元素的基线与父元素的上标基线对齐
* text-top: 使元素的顶部与父元素的字体顶部对齐
* text-bottom: 使元素的顶部与父元素的字体底部对齐
* middle:使元素的中部与父元素的基线加上父元素x-height（译注：x高度）的一半对齐
* length values: 相对于父元素基线
* percentage values: 相对于父元素基线

相对于行：
* top:使元素及其后代元素的顶部与整行的顶部对齐
* bottom:使元素及其后代元素的顶部与整行的底部对齐

#### img底部留有空白问题
原因：图片默认和x底部基线对齐
解决方法：

1、display: block;

2、vertical-align: middle;

3、设置足够小的line-height

4、line-height为相对单位（150%，1.5），font-size间接控制：font-size:0;
注：font-size可解决x基线产生的误差


#### 图片+文字竖直居中问题
```
<div class="parent-div" href="index-undfined.html">
    <img src="image/1.jpg" alt="">
    <span>test</span>
</div>

 .parent-div{
      line-height: 100px;
      font-size: 0;
      background-color: #ddd;
  }
  .parent-div img{
      vertical-align: middle;
      width: 60px;
  }
   .parent-div span{
       display: inline-block;
       line-height: normal;
       vertical-align: middle;
       font-size: 36px;
   }
```

#### 相邻行内元素文字竖直居中问题
行内元素的vertical-align属性会影响父元素的基线
```
<div class="parent-div2">
    <span>child 1</span>
    <span>
        <div class="big">big</div>
        <div class="small">child 2</div>
    </span>
</div>

 .parent-div2>span{
            display: inline-block;
            vertical-align: middle;
        }
        .big{
            font-size: 36px;
        }
```



#### 参考
[MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/vertical-align)

[CSS深入理解vertical-align和line-height的基友关系](https://www.zhangxinxu.com/wordpress/2015/08/css-deep-understand-vertical-align-and-line-height/)
