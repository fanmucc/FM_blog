> 前期准备
- 安装`node`
- 进入创建的文件夹 运行`npm init` 生成 `package.json`文件
- 安装webpack `npm install webpack webpack-cli -D`
- 创建 `webpack.config.js` 文件

#### `entry`打包入口文件及`output`输出文件路径

``` js
// webpack.config.js
let path = require('path')

module.exports = {
    mode: 'development',
    entry: './src/index.js',                // 打包入口文件目录
    output: {
        filename: 'bundle.js',               // 打包生成的文件名
        path: path.resolve(__dirname, 'dist')  // 打包的文件所在的文件夹， 没有创建的话会自动创建
    }
}
```

#### `output` 多入口配置
- 生成多个js文件

``` js
// webpack.config.js
module.exports = {
    mode: 'development',
    entry: {
        index: './src/index.js',
        app: './src/app.js'
    },
    output: {
        filename: [name].js,      // 通过 [name] 占位符来确保文件名称的唯一性
        path: path.resolve(__dirname, 'dist')
    }
}
```

