#### Koa 框架介绍
Node.js 是一个异步的世界，官方 API 支持的都是 callback 形式的异步编程模型，这 会带来许多问题，例如:1、callback 嵌套问题 2、异步函数中可能同步调用 callback 返回 数据，带来不一致性。为了解决以上问题 Koa 出现了。
> Koa -- 基于 Node.js 平台的下一代 web 开发框架

koa 是由 Express 原班人马打造的，致力于成为一个更小、更富有表现力、更健壮的 Web 框架。 使用 koa 编写 web 应用，可以免除重复繁琐的回调函数嵌套， 并极大地提 升错误处理的效率。koa 不在内核方法中绑定任何中间件， 它仅仅提供了一个轻量优雅的 函数库，使得编写 Web 应用变得得心应手。开发思路和 express 差不多，最大的特点就是 可以避免异步嵌套。

#### 安装
```npm install koa -G```

#### 使用
```
1. 初始化项目
npm init;
2. 安装koa
npm install --save koa;
3. 引入
/引入 Koa
const koa=require('koa'); const app=new koa();
//配置中间件 (可以先当做路由) app.use( async (ctx)=>{ ctx.body='hello koa2'
})
//监听端口 app.listen(3000);
```