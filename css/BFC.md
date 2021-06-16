### BFC
块格式化上下文（Block Formatting Context，BFC）,可看做是隔离了的独立容器

下列方式会创建块格式化上下文：

* 根元素或包含根元素的元素
* 浮动元素：元素的 float 不是 none
* 绝对定位元素：position: absolute || fixed
* overflow 值不为 visible 的块元素
* contain 值为 layout、content或 strict 的元素
* display为inline-block、table-**、flow-root、flex、grid的元素

   行内块元素（元素的 display 为 inline-block）

   表格单元格（元素的 display为 table-cell，HTML表格单元格默认为该值）

   表格标题（元素的 display 为 table-caption，HTML表格标题默认为该值）

   匿名表格单元格元素（元素的 display为 table、table-row、 table-row-group、table-header-group、table-footer-group（分别是HTML table、row、tbody、thead、tfoot的默认属性）或 inline-table）

   弹性元素（display为 flex 或 inline-flex元素的直接子元素）

   网格元素（display为 grid 或 inline-grid 元素的直接子元素）

* 多列容器（元素的 column-count 或 column-width 不为 auto，包括 column-count 为 1）
* column-span 为 all 的元素始终会创建一个新的BFC，即使该元素没有包裹在一个多列容器中（标准变更，Chrome bug）。


#### BFC 特性&应用
* 浮动定位和清除浮动时只会应用于同一个BFC内的元素
* 浮动不会影响其它BFC中元素的布局
* 外边距折叠只会发生在属于同一BFC的块级元素之间
* 阻止元素被浮动元素覆盖，应用：实现两列自适应布局，左边的宽度固定，右边的内容自适应宽度
```
<div style="overflow: auto">
    <div style="height: 100px;width: 100px;float: left;background: lightblue">
        我是一个左浮动的元素
    </div>
    <div style=" height: 80px;background: #eee;overflow: auto">
        我是一个没有设置浮动, 也没有触发 BFC 元素, width: 200px; height:200px; background: #eee;
    </div>
</div>
```

注意：外边距折叠发生条件：
* 都是普通流中的元素且属于同一个 BFC
* 没有被 padding、border、clear 或非空内容隔开
* 两个或两个以上垂直方向的「相邻元素」

### IFC
内联格式化上下文（Inline Formatting Contexts）

应用：

水平居中：当一个块要在环境中水平居中时，设置其为inline-block则会在外层产生IFC，通过text-align则可以使其水平居中。

垂直居中：创建一个IFC，用其中一个元素撑开父元素的高度，然后设置其vertical-align:middle，其他行内元素则可以在此父元素下垂直居中。


### GFC
网格布局格式化上下文（GridLayout Formatting Contexts）

display:grid



### FFC
自适应格式化上下文（Flex Formatting Contexts）

display:flex


### 兼容性
* BFC： css2
* IFC：css2
* GFC：css3，IE10+
* FFC：css3，IE10+


### position && overflow:hidden
记住这个：position: absolute元素溢出overflow: hidden元素的时候，如果其第一个含有position属性(static除外)的祖先元素（一直到body）是overflow: hidden元素祖先元素的时候，则不隐藏；否则，隐藏。

或者记住这个：火星人在地球触发了法律，如果火星人的老爸在这法律之外，则这个火星人啥事没有；否则，坐牢！

```
body
    height: 0; overflow: hidden;
        position: absolute; /* 不会被隐藏 */
```

```
position: relative;
    height: 0; overflow: hidden;
        position: absolute; /* 不会被隐藏 */
```

```
height: 0; overflow: hidden;  position: relative;
    position: absolute; /* 会被隐藏 */
```

```
height: 0; overflow: hidden;
    position: relative;
        position: absolute; /* 会被隐藏 */
```

[您可能不知道的CSS元素隐藏“失效”以其妙用 张鑫旭](https://www.zhangxinxu.com/wordpress/2012/02/css-overflow-hidden-visibility-hidden-disabled-use/)
