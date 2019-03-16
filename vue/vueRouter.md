# vue-router

## 定义

  1. 定义路由组件

          // 可以从其他文件 import 进来

          const Foo = { template: '<div>foo</div>' }
          const Bar = { template: '<div>bar</div>' }

  2. 定义路由

 // 每个路由应该映射一个组件。 其中"component" 可以是
// 通过 Vue.extend() 创建的组件构造器，

    const routes = [
    { path: '/foo', component: Foo },
    { path: '/bar', component: Bar }
    ]
    // 或者，只是一个组件配置对象。
    // 我们晚点再讨论嵌套路由。

  3. 创建 router 实例，然后传 `routes` 配置

    const router = new VueRouter({
      routes // (缩写) 相当于 routes: routes
    })

  4. 创建和挂载根实例。

  // 记得要通过 router 配置参数注入路由，

  // 从而让整个应用都有路由功能

    const app = new Vue({
      router
    }).$mount('#app')


## 组件

* router-view

* 嵌套路由  children属性

* 导航 
  
  * 编程式 
  
      router.push   
      router.replace
      router.go

  * 声明式 router-link

  * meta

