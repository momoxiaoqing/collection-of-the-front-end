### mixins
mixins中全局变量不独立于混入的组件，即：在组件1中若对全局变量global做修改，在组件2中混入时，修改仍在

#### extend & mixins & extends 区别
* extend用于创建vue实例
* mixins可以混入多个mixin，extends只能继承一个
* mixins类似于面向切面的编程（AOP），extends类似于面向对象的编程
* 优先级Vue.extend>extends>mixins