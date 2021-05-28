### prop父子组件间数据交互
* 组件的调用顺序都是先父后子
* 渲染完成的顺序是先子后父
* 组件的销毁操作是先父后子
* 销毁完成的顺序是先子后父

1、父子组件通信

* 父->子props；子（emit）->父（on）
* 获取父子组件实例 $parent / $children 如：直接在子组件的methods方法里面写：this.$parent.show()//show为父组件中定义的方法
* Ref (如果在普通的 DOM 元素上使用，引用指向的就是 DOM 元素；如果用在子组件上，引用就指向组件实例)，如在引入的子组件的标签上挂载一个： ref="comA"，然后在方法中或者子组件的数据，this.$refs.comA.titles
* Provide、inject 官方不推荐使用，但是写组件库时很常用

2、兄弟组件通信

* Event Bus 实现跨组件通信: Vue.prototype.$bus = new Vue()
* Vuex
```
// 在main.js中把实例化的vue对象放在vue的原型上
Vue.prototype.$bus = new Vue() 
// 新建bus文件,再引用也可以：
// import Vue from 'vue'; export default new Vue();

// 子组件一
methods:{
    sendData(){
        this.$bus.$emit("send",this.childOneData)
    }
}

// 子组件二
created(){
    this.$bus.$on("send",(payload)=>{
        console.log("来自兄弟组件的数据",payload)
        this.msg = payload
    })
}
```

3、跨级组件通信

* Vuex
* attrs,listeners
* Provide、inject

### 父组件监听到子组件的生命周期
$emit触发：
```
// Parent.vue
<Child @mounted="doSomething"/>

// Child.vue
mounted() {
  this.$emit("mounted");
}
```

```

```

### prop传递的对象修改

1、data定义局部变量，其值为prop，不是引用复制

```
props: ['initialCounter'],
data: function () {
  return { counter: this.initialCounter }   //counter不会随着initialCounter 的变化而变化
}
```

2、computed返回prop，是引用复制，但当size.test初始值为undefined时，就不会被监听，即normalizedSize不会随着size.test

的变化而变化

```
props: ['size'],
computed: {
  normalizedSize: function () {
    return this.size.test
  }
}
```





