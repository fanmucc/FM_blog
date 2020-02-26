#### 文件指纹
> 打包后输出的文件名的后戳

|占位符名称|含义|
|:---:|:---|
|[ext]|资源后辍名|
|[name]|文件名称|
|[path]|文件的相对路径|
|[folder]|文件所在的文件夹|
|[contenthash]|文件的能容hash,默认是md5生成,长度为20|
|[hash]|文件内容的hash,默认是md5生成,长度为32|
|[emoji]|一个随机的指代文件内容的emoj|


!> 文件指纹` chunkhash` 无法和热更新一起使用，测试时应先隐藏 `webpack-dev-server` 等配置

- 版本管理
- 更新后缓存使用

##### 如何生成文件指纹
- `Hash`: 和整个项目的构建相关，只要项目文件有改动，整个项目构建的 `hash` 值就会变动;
- `Chunkhash`: 和 `webpack` 打包的 `chunk` 有关， 不同的 `entry` 会生成不同的 `chunkhash` 值;
- `Contenthash`: 根据文件内容来定义 `hash` ，文件内容不变，则 `contenthash` 不变;

一般 `JS` 文件使用 `Chunkhash`， `CSS` 文件使用 `Contenthash`;

##### JS文件指纹设置
``` js
// webpack.config.js
module.exports = {
    output: {
        filename: '[name]_[chunkhash:8].js',    // chunkhash: 8  chunkhash的长度为20为  :8 表示只截取前8位
        path: path.join(__dirname, '/dist')
    }
}
```

##### 文件指纹设置
``` js
// webpack.config.js
module.exports = {
    module: {
        rules: [
            test: '.(png|jpg|gif|jpeg)$/,
            use: {
                loader: 'file-loader',
                options: {
                    name: '[name]_[hash:8][ext]'    // 文件的hash长度为 32 位
                }
            }
        ]
    }
}
```

##### CSS指纹设置
因为要将`css`独立出文件来，需要借助插件

- `npm i mini-css-extract-plugin -D`

``` js
const MiniCssExtractPlugin =  require('mini-css-extract-plugin');
    module.exports = {
        module: {
        rules: [
            {
                test: /.less$/,
                use: [
                    MiniCssExtractPlugin.loader,        // style-loader 是将css插入到Dom中， 而此次需要独立出文件，所以进行替换
                    'css-loader',
                    'less-loader'
                ]
            },
        ]
    },
    plugins: [
        new MiniCssExtractPlugin({
            filename: '[name]_[contenthash:8].css'     // contenthash 长度为20
        })
    ]
}

```

