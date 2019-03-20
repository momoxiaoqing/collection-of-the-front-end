### 概念
* attribute :特性，XML 元素中的概念，用于描述 XML 标签的附加信息，即：XML 标签的特性； 如：```<input type="text" value="初始值"/> ```中的 type、value 均是input元素的特性;
* property :属性，JavaScript 对象的概念，即：JavaScript 对象的属性，如: JavaScript 对象 var person = {name:"郭斌勇",age:28} 中的 name、age 均是对象 person 的属性；

### 关联
attribute：html的成员；

property： 由html转化的Dom 的成员

例：对于 Dom 对象，dom.checked 的值始终是布尔类型的，dom.value 的值始终是相应 input 元素的当前值，并非是 HTML 中 input 元素的 value 特性的值，dom.defaultValue 则是 HTML 中 input 元素的 value 特性的值；


