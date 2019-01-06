### table的border问题123

* border-width不同时，较大者边框样式将被渲染；

  ```
   border-width不相同时，border-style优先级：hidden &gt; double &gt;solid &gt; dashed &gt;dotted &gt;none（默认值）
  ```

* table-border优先级： 'table-cell'，'table-row'，'table-row-group'，'table-col'，'table-col-group', 'table'

* 左上优先渲染原则

* border-style:double四个角的渲染方式：

![](/assets/border-style.png)

* border-style:double;宽度需要大于等于3px才能体现，否则，样式与solid无异

  ```
   border-style:double;会发生溢出，并且左右溢出值不一致
  ```

* 四个角重合之处采用组合层叠的方式进行渲染，而不是单一的选择某一种样式

而四条边框则非重合（单一选择某一条边进行渲染）

