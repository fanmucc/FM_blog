#### 路由守卫

> `vue-router` 提供的导航守卫主要用来通过跳转或取消的方式守卫导航。有多种机会植入路由导航过程中：全局的, 单个路由独享的, 或者组件级的。

路由守卫流程

- 1. 导航被触发
- 2. 在失活的组件(即将离开的页面组件)里 调用离开路由守卫 `beforeRouteLeave`;
- 3. 调用全局的前置路由守卫 `beforeEach`;
- 4. 在重用的组件里调用 `beforeRouteUpdate`;
- 5. 调用路由独享的守卫 `beforeEnter`;
- 6. 解析异步路由组件;
- 7. 在被激活的组件(即将进入的页面组件)里 调用 `beforeRouteEnter`;
- 8. 调用全局的解析路由 `beforeResolve`;
- 9. 导航被确认;
- 10. 调用全局的后置守卫 `afterEach`;
- 11. 触发DOM更新;
- 12. 用创建好的实例调用 `beforeRouteEnter` 守卫里传给 `next` 的回调函数;

分类

路由守卫又分为全局路由守卫和组件路由守卫即路由独享守卫三种

- 全局路由守卫
> `beforeEach`  `beforeResolve` `afterEach`

- 路由独享守卫
> `beforeEnter`

- 组件内守卫
> `beforeRouteEnter` `beforeRouteUpdate` `beforeRouteLeave`

详解

`beforeEach` 全局前置守卫

```js
router.beforeEach((to, from, next) => {
    // ...
})
```
三个参数: 
    1. `to` 即将要进入的目标路由; 
    2. `from` 当前导航正要离开的路由; 
    3. `next`: `next()`进入下一个钩子,进行路由跳转, `next(false)`中断当前的导航, `next('/')或next({path: '/'})` 会进入一个不同的地址,不会走`to`参数的目标路由,进入一个新的导航,你可以向 `next` 传递任意位置对象，且允许设置诸如 `replace: true、name: 'home'` 之类的选项以及任何用在 `router-link` 的 `to` `prop` 或 `router.push` 中的选项。 `next(error)`: (2.4.0+) 如果传入 `next` 的参数是一个 `Error` 实例，则导航会被终止且该错误会被传递给 `router.onError()` 注册过的回调。

确保要调用 `next` 方法;

`beforeResolve` 全局解析守卫

```js
router.beforeResolve((to, from, next) => {
    // ...
})
```

你可以用 `router.beforeResolve` 注册一个全局守卫。这和 `router.beforeEach` 类似，区别是在导航被确认之前，同时在所有组件内守卫和异步路由组件被解析之后，解析守卫就被调用。

`afterEach` 全局后置钩子

```js
router.afterEach((to, from) => {
    // ...
})
```
和前置守卫不同,不需要 `next`参数,因为已经跳转结束, 在这里我们可以处理一些跳转完成后的事务,如 iview ui 中 afterEach加载进度条,可以在`router.beforeEach`中设置开启, 在`router.afterEach`设置结束;


`beforeEnter` 路由独享守卫

你可以在路由配置上直接定义 `beforeEnter` 守卫

```js
const router = new VueRouter({
  routes: [
    {
      path: '/foo',
      component: Foo,
      beforeEnter: (to, from, next) => {
        // ...
      }
    }
  ]
})
```

这些守卫与全局前置守卫的方法参数是一样的

组件内路由守卫

- beforeRouteEnter
- beforeRouteUpdate
- beforeRouteLeave

```
const Foo = {
  template: `...`,
  beforeRouteEnter (to, from, next) {
    // 在渲染该组件的对应路由被 confirm 前调用
    // 不！能！获取组件实例 `this`
    // 因为当守卫执行前，组件实例还没被创建
  },
  beforeRouteUpdate (to, from, next) {
    // 在当前路由改变，但是该组件被复用时调用
    // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
    // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
    // 可以访问组件实例 `this`
  },
  beforeRouteLeave (to, from, next) {
    // 导航离开该组件的对应路由时调用
    // 可以访问组件实例 `this`
  }
}
```
`beforeRouteEnter` 守卫 不能 访问 `this`，因为守卫在导航确认前被调用,因此即将登场的新组件还没被创建。

不过，你可以通过传一个回调给 next来访问组件实例。在导航被确认的时候执行回调，并且把组件实例作为回调方法的参数。

```
beforeRouteEnter (to, from, next) {
  next(vm => {
    // 通过 `vm` 访问组件实例
  })
}
```
注意 `beforeRouteEnter` 是支持给 `next` 传递回调的唯一守卫。对于 `beforeRouteUpdate` 和 `beforeRouteLeave` 来说，`this` 已经可用了，所以不支持传递回调，因为没有必要了;

```
beforeRouteUpdate (to, from, next) {
  // just use `this`
  this.name = to.params.name
  next()
}
```

这个离开守卫通常用来禁止用户在还未保存修改前突然离开。该导航可以通过 `next(false)` 来取消

```

beforeRouteLeave (to, from , next) {
  const answer = window.confirm('Do you really want to leave? you have unsaved changes!')
  if (answer) {
    next()
  } else {
    next(false)
  }
}

```