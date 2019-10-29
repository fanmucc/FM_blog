#### 路由

vue-router是Vue.js官方的路由插件，它和vue.js是深度集成的，适合用于构建单页面应用。vue的单页面应用是基于路由和组件的，路由用于设定访问路径，并将路径和组件映射起来。传统的页面应用，是用一些超链接来实现页面切换和跳转的。在vue-router单页面应用中，则是路径之间的切换，也就是组件的切换。

#### hast 和 history 两种模式

vue-router 默认`hast`模式-- 使用URL的hash来模拟一个完成的URL,当URL发生改变时,页面不会重新加载

- `hast` 地址栏中`#`号符, 如: http://abc/#/home ; hash值为'#', 特点为当URL发生改变时,页面不会重新进行加载;
- `history` 其利用HTML5 History Interface 中新增的 `pushState()` 和 `replaceState()` 方法; 使用此方法也无需重新加载页面; 当使用`history`模式时 URL就像正常的url, 如: http://abc/home ; 但是这种模式还需要后台配置的支持,因为应用为单页面应用,如果后台没有正确的配置,当用户在浏览器直接访问 http://oursite.com/user/id; 就会返回`404`, 所以要在服务端添加一个覆盖所有情况的候选资源: 如果URL匹配不到任何静态资源,则应该返回同一个 index.html 页面, 这个页面就是app所依赖的页面;

配置方法

router.js文件下
```js
const router = new VueRouter({
    mode: 'history',        // 当不进行设置时,默认为hast模式;
})
```

#### 路由配置

我们要进行引入 `vue-router` 和 `vue` 插件
```js
import Vue from 'vue';
import Router from 'vue-router';
import Home from '@/views/Home.vue'
const router = new Router({
    routes: [
        {
            path: '/home',
            component: Home
        },
        {
            ...
        }
    ]
})
```
还可以将路由文件拆开单独来进行设置
```js
// routers.js // 路由文件
import Home from '@/views/Home.vue'
const routers = [
    {
        path: '/home',
        component: Home
    },
    {

    }
];

// router.js 文件
import Vue from 'vue';
import Router from 'vue-router';
import routes from './routers';   //单独定义的路由文件

const router = new Router({
    routes: routes,     // 可以简写成 routes
})
```

#### 动态匹配路由

```js
const router = new Router({
    routes: [
        {
            path: '/user/:id',
            component: User,
        }
    ]
})
```
现在当 `/user/foo`和`/user/bar` 都将映射到相同的路由;

一个`"路由参数"`使用冒号`:`标记,当匹配到一个路由时,参数值会被设置到`this.$route.params`来接受到`:`后的内容.
```js
// URL: http://abc/user/12
<template>
    <p>{{ this.$route.params.id }}</p>      // 输出为12
</template>
```

###### 动态路由参数发生变化

当使用路由参数时，例如从 `/user/foo` 导航到 `/user/bar`，原来的组件实例会被复用。因为两个路由都渲染同个组件，比起销毁再创建，复用则显得更加高效。不过，这也意味着组件的生命周期钩子不会再被调用;

复用组件时，想对路由参数的变化作出响应的话，你可以简单地 `watch` (监测变化) `$route`对象;

```js
const User = {
  template: '...',
  watch: {
    '$route' (to, from) {
      // 对路由变化作出响应...
    }
  }
}
```
或者使用 2.2 中引入的 `beforeRouteUpdate` 导航守卫：

```js
const User = {
  template: '...',
  beforeRouteUpdate (to, from, next) {
    // react to route changes...
    // don't forget to call next()
  }
}
```
#### 嵌套路由

嵌套路由在日常应用界面比较常见, 如: 后台管理系统,当切换侧边栏的时候只是内容展示区做了相应的变化,页面头部和侧边栏都不会进行变动;

```js
const router = new Router({
    routes: [
        path: '/user',
        component: User,
        children: [
            {
                path: 'child',
                component: User_child
            }
        ]
    ]
}) 
```
页面渲染

```js
    // 使用
    <router-view></router-view>
```

#### 路由命名\重定向和别名

##### 命名

通过一个名称来标识一个路由显得更方便一些，特别是在链接一个路由，或者是执行一些跳转的时候;

设置命名: 属性名: name

```js
{
    path: 'home',
    name: 'home',
    component: User
}
```

``` router.push('home') / router.push({name: 'home', params: {userId: 123 }})```;

##### 重定向

设置重定向: 属性名: redirect

```js
{
    path: 'home',
    redirect: '/',
    component: User
}
```

重定向为,当我们访问重定向的路由名时,会返回到我们设置的`redirect`路径下, 即当我们访问 `home` 这个路由路径时,会跳转到`/`这个路径;

也可以携带参数

```js
{
    path: 'home',
    redirect: to => {
        return {name: '/'}
    },
    component: User
}
```
##### 别名

“重定向”的意思是，当用户访问 `/a`时，URL 将会被替换成 `/b`，然后匹配路由为 `/b`;

那么“别名”又是什么呢？

`/a` 的别名是 `/b`，意味着，当用户访问 `/b` 时，URL 会保持为 `/b`，但是路由匹配则为 `/a`，就像用户访问 `/a` 一样。
如同人的名字一样,一个大名一个小名,所以都是指定的为同一个人;

```js

const router = new VueRouter({
  routes: [
    { path: '/a', component: A, alias: '/b' }
  ]
})

```




