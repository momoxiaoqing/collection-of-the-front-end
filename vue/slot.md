###插槽

* 内容：
   * 插槽内可以包含任何模板代码，包括 HTML、组件；
   * 插槽模板中没有包含一个 <slot> 元素，则该组件起始标签和结束标签之间的任何内容都会被抛弃
* 作用域：父级模板里的所有内容都是在父级作用域中编译的；子模板里的所有内容都是在子作用域中编译的
* 后备内容：默认渲染内容，在`<slot></slot>`中
* 具名插槽：v-slot:header，缩写为#header
  * 不带 name 的 <slot> 出口会带有隐含的名字“default”
  * v-slot 只能添加在 \<template> 上，除了当被提供的内容只有默认插槽时 
    * 默认插槽的缩写语法不能和具名插槽混用，因为它会导致作用域不明确
      ```vue
      <!-- 无效，会导致警告 -->
      <current-user v-slot="slotProps">  //默认插槽的缩写语法
        {{ slotProps.user.firstName }}
        <template v-slot:other="otherSlotProps">
          slotProps is NOT available here
        </template>
      </current-user>
      ```
      
* 插槽 Prop：作用域插槽的内部工作原理是将你的插槽内容包裹在一个拥有单个参数的函数里
  ```
  function (slotProps) {
    // 插槽内容
  }
  ```
  v-slot 的值实际上可以是任何能够作为函数定义中的参数的 JavaScript 表达式
  ```vue
  <current-user v-slot="{ user }">
  {{ user.firstName }}
  </current-user>
  
  // prop 重命名
  <current-user v-slot="{ user: person }">
  {{ person.firstName }}
  </current-user>
  
  //定义后备内容
  <current-user v-slot="{ user = { firstName: 'Guest' } }">
  {{ user.firstName }}
  </current-user>
  ```