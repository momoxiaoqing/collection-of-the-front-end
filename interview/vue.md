### vue相关
* [生命周期图示](../assets/lifecycle.png)
* [组件相关](../vue/zu-jian.md)
* [vue3变化简单说明](../assets/Vue-3-Cheat-Sheet.pdf)


### vue数据双向绑定的原理
* 实现一个监听器 Observer对数据对象进行遍历，包括子属性对象的属性，利用 Object.defineProperty() 对属性都加上 setter 和 getter。这样的话，给这个对象的某个值赋值，就会触发 setter，那么就能监听到了数据变化。
* 实现一个解析器 Compile解析 Vue 模板指令，将模板中的变量都替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，调用更新函数进行数据更新。
* 实现一个订阅者 Watcher：Watcher 订阅者是 Observer 和 Compile 之间通信的桥梁 ，主要的任务是订阅 Observer 中的属性值变化的消息，当收到属性值变化的消息时，触发解析器 Compile 中对应的更新函数。
* 实现一个订阅器 Dep订阅器采用 发布-订阅 设计模式，用来收集订阅者 Watcher，对监听器 Observer 和 订阅者 Watcher 进行统一管理。

### v-model原理
```
<input v-model='something'>
```
相当于
```
<input v-bind:value="something" v-on:input="something = $event.target.value">
```
### Proxy和Object.defineProperty的区别
* proxy可以直接监听对象而非属性
* proxy拦截方法较多，如：has,apply,construct,ownkeys
* proxy返回值为对象实例，而object.property只能遍历对象属性直接修改


### keep-alive 实现列表缓存
props:
* include:字符串或正则表达式，组件内命名的name
* exclude:字符串或正则表达式，组件内命名的name
* max:

```
<keep-alive include="company-list,abnormal-list">
    <router-view :key="$route.fullPath"/>
</keep-alive>
```
不需要缓存的时候，进入页面：`:to="{name:'companyList',query:{randomID:Math.random()}}"`，否则go(-1)