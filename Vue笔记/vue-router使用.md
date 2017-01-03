## vue-router插件使用
* 说明
  * 官方提供的用来实现SPA的插件
  * github: https://github.com/vuejs/vue-router
  * 对应vue1.x的版本为: 0.7.13
* 下载和引入
  ```
  npm install vue-router@0.7.13 --save
  import VueRouter from 'vue-router'
  ```
* 相关API说明
  * VueRouter(): 构建函数, 用来创建路由器对象
    * 配置: 在创建对象时可以指定一个配置对象
      ```
      new VueRouter({
        linkActiveClass: 'active', //指定当前路由链接的样式名
        history: true //去掉#!
      })
      ```
    * map(): 映射路由
      ```
      router.map({
          '/about': {
            component: About
          },
          '/home': {
            component: Home
          }
        })
      ```
    * start(): 启动应用
      ```
      router.start(App, '#app')
      ```
    * go(): 请求指定路由
      ```
      router.go('/about')
      ```
  * 指令与组件:
    * v-link: 用来指定路由路径
      ```
      <a v-link='{path:"/about"}'>About</a>
      ```
    * <router-view>: 用来显示当前路由组件界面
      ```
      <router-view></router-view>
      ```
* 实现简单路由
  * 路由组件:
    * home.vue
    * about.vue
  * 应用组件: App.vue
    ```
    <div>
      <!--路由链接-->
      <a v-link="{path:'/about'}">About</a>
      <a v-link="{path:'/home'}">Home</a>
      <!--用于渲染当前路由组件-->
      <router-view keep-alive></router-view>  
    </div>
    ```
  * 入口js: main.js
    ```
    import Vue from 'vue'
    import VueRouter from 'vue-router'
    import app from './components/app.vue'
    
    //使用插件
    Vue.use(VueRouter)
    
    //创建用来映射路由的路由器对象
    const router = new VueRouter({
      linkActiveClass: 'active', //指定当前路由链接的样式名
      history: true //去掉#!
    })
    
    //配置路由
    router.map({
      '/about': {component: about},
      '/home': {component: home}
    })
    
    //启动应用
    router.start(app, '#app')
    
    //初始请求一个路由
    router.go('/about')
    ```
* 实现嵌套路由
  * 配置嵌套路由
    ```
    subRoutes: {
      '/news': {
        component: news
      }
    }
    ```
  * 路由路径
    ```
    <a v-link="{path: '/home/news'}">News</a>
    ```
* 路由请求携带参数
  * 配置路由
    ```
    subRoutes: {
      '/mdetail/:id': {
        component: messageDetail
      }
    }
    ```
  * 路由路径
    ```
    <a v-link="{path: '/home/message/mdetail/2'}">{{m.title}}</a>
    ```
  * 路由组件中读取请求参数
    ```
    {{$route.params.id}}
    ```
* <route-view>使用
  * 参数keep-alive属性实现路由界面的缓存
  * 通过标签属性可动态向路由组件内部传递数据
    ```
    <router-view keep-alive :msg="msg"></router-view>
    ```
    在router-view里面有可能有多个组件时，在用router-view里面传递属性的时候，在里面包含的
    组件里面使用的时候，必须在router-view里面的组件用props声明