### 公共组件的加载
在写管理后台的时候，我们往往需要在login页面不显示头部组件，其他页面都显示，在此记录下可行的几种方法：
* 实时监控当前路由（watch || components）
* 路由配置（嵌套命名视图 || 命名视图）

#### 实时监控当前路由（watch/components）
用v-show || v-if控制header的显示，用watch || components监控页面路由，若当前路由不是login则显示，否则隐藏

#### 路由配置
路由配置可分为嵌套命名视图和命名视图

**1、嵌套命名视图**

index.vue中引用header组件， router配置如下：
```
routes: [
    {
        path: '/login',
        name: 'login',
        component: () => import( './views/login')
    },
    {
        path: '/',
        name: 'index',
        component: () => import( './views/index'),
        children: [
            {
                path: '/a',
                name: 'a',
                component: () => import( './views/a')
            },
            {
                path: '/b',
                name: 'b',
                component: () => import( './views/b')
            }
        ]
    }
]
```

**2、命名视图**

App.vue中：
```
 <div id="app">
    <router-view/>
    <router-view name="header"/>
 </div>
```
路由配置：
```
 routes: [
     {
         path: '/login',
         name: 'login',
         component: () => import( './views/login')
     },
     {
         path: '/a',
         name: 'a',
         // component: () => import( './views/home')
         components: {
             default:  () => import( './views/a'),
             header:  () => import( './views/header'),
         }
     },
     {
         path: '/b',
         name: 'b',
         components: {
             default:  () => import( './views/b'),
             header:  () => import( './views/header'),
         }
     }
]
```

以上2种配置的效果类似：访问/a和/b时都会加载header
