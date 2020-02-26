#### css px转rem

> `px2rem-loader` `lib-flexible`

``` js
module.exports = {
    module: {
        rules: [
            {
                test: /.css$/,
                use: [
                    MiniCssExtractPlugin.loader,        // 将css分离出文件
                    "css-loader",
                    {
                        loader: "px2rem-loader",
                        options: {
                            remUnit: 75,                // 基础的像素比值
                            remPrecision: 8             // 计算后rem值截取到小数点的后8位
                        }
                    },
                    {
                        loader: "postcss-loader",
                        options: {                      // loader参数配置
                            plugins: [
                                require('autoprefixer')
                            ]
                        }
                    }
                ]
            }
        ]
    }
}
```

转化`rem` 完成后， 将`lib-flexible`中的`js`文件一如到打包后的`html`文件头部, 就可以适配不同分辨率的浏览器了；


如果不想讲特定的`px`进行转化
```css
.page {
  font-size: 12px; /*no*/
  width: 375px; /*no*/
  height: 40px;
}
```