#### 文件监听
webpack 开启监听模式一般有两种
- 启用`webpack`命令时， 带上 `--watch` 参数；
- 在配置 `webpack.config.js` 中设置 `watch: true`；

``` js
// webpack.config.js
watch: true,                // 默认为 false
watchOptions: {             // 只有开启监听模式 watchOptions 才有意义
    ignored: /node_module/, // 默认为空，不监听的文件或者文件夹，支持正则匹配
    aggregateTimeout: 300,  // 监听到变化发生后等300毫秒后再去执行， 默认为300毫秒
    poll: 1000              // 判断文件是否发生变化是不断的询问系统指定文件有没有发生变化实现的，默认每秒问1000次
},
```


#### 文件热更新 `webpack-dev-server`

- 安装 `webpack-dev-server` `npm install webpack-dev-server`
- 在`package.json` 的 `scripts` 中配置

``` json
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack --config webpack.config.js",
    "dev": "webpack-dev-serve",
    "dev": "webpack-dev-serve --open"   // 会在运行后自动打开页面
  },
```

`webpack-dev-server` 配置

!> 不进行配置时，进入的为文件目录，需要手动点击到打包目录才能查看效果；

``` js
// 引入webpack
const webpack = require('webpack');

plugins: [
    new webpack.HotModuleReplacementPlugin({
        multiStep: true,            // 布尔值,如果为true，则插件将分两步构建-首先编译热更新块，然后编译其余的常规资产。
        fullBuildTimeout: 200,      // 数字,multiStep启用时两步之间的延迟
        requestTimeout: 1000        // 数字,用于清单下载的超时（自webpack 3.0.0起）
        // 这些选项是实验性的，可能不建议使用。如上所述，它们通常不是必需的, new webpack.HotModuleReplacementPlugin()就足够了。
    })
],
devServer: {                                        // 配置开发server 随着用户的保存自行运行刷新页面
    contentBase: path.resolve(__dirname, "./dist"), // 运行目录  
    progress: true,                                 // 打包时的进度条
    port: 9000                                      // 端口号
},      
```