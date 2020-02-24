> [NPM地址](https://www.npmjs.com/products/teams?utm_source=adwords&utm_medium=ppc&utm_campaign=npmTeams2019Q2&utm_content=site&gclid=EAIaIQobChMIw-fbptrp5wIV2aiWCh1LjQPzEAAYASAAEgLm4fD_BwE)

#### 概念
本质上，`webpack` 是一个现代 `JavaScript` 应用程序的静态模块打包器(`module bundler`)。当 webpack 处理应用程序时，它会递归地构建一个依赖关系图(`dependency graph`)，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 `bundle`

#### 通过 `npm run` 来运行webpack
``` json
// package.json
"script" : {
    "build": "webpack --config webpack.config.js"
}

```
#### webpack 配置组成
``` js
module.exports = {
    entry: './src/index.js',            // 打包的入口文件
    output: './dist/main.js',           // 打包的输出
    mode: 'production',                 // 打包环境
    module: [                           // Loader 配置
        rules: [
            {
                test: /.\txt$/,
                use: 'raw-loader'       // loader 执行顺序为从右到左，从下倒上
            }
        ]
    ],
    plugins: [
        new HtmlwebpackPlugin({         // 插件配置
            template: '/src/index.html'
        })
    ]
}
```
#### `mode`
开发环境和生产环境设置

只接受两个值`development` 开发环境与 `production`生产环境

通过选择 `development` 或 `production` 之中的一个，来设置 `mode` 参数，你可以启用相应模式下的 `webpack` 内置的优化

#### `Loaders`核心概念
`webpack` 开箱即用只支持 `JS` 和 `JSON` 两种文件类型， 通过 `loaders` 去支持其他文件类型并且把他们转化成有效的模块，并且可以添加到依赖图中

本身是一个函数，接受源文件作为参数，返回转换的结果

#### `Plugins`核心概念
插件用于 `bundle` 文件的优化，资源管理和环境变量的注入，作用于整个构建过程