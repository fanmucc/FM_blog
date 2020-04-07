#### 页面跳转
> 微信页面主要分为两种页面: tabbar页面与普通page页面

### tabbar页面跳转
``` js
    wx.swtichTab({
        url,  // tabbar页面路径
        success: () => {
            // 成功跳转的回调参数
        },
        fail: () => {
            // 失败的回调参数
        },
        complete: () => {
            // 不管成功或者失败都会调用
        }
    })
```

### page页面跳转

- 不能跳转到tabbar页面
- 会将跳转的页面保存至页面栈

``` js
    wx.navigateTo({
        url, //   可以携带参数，如： '/pages/goods/goods?id=1&name=fanmu'
        success: () => {
            // 成功调用
        },
        fail: () => {
            // 失败调用
        },
        complete: () => {
            // 成功或者失败都进行调用
        }
    })
```

### 关闭当前页面返回上一页或者多页
- 带测试
``` js
    wx.navigateBack({
        url,  // 直接指定返回的页面
        data: number,  // 设置返回的页数
        success: () => {
            // 成功调用
        },
        fail: () => {
            // 失败调用
        },
        complate: () => {
            // 成功或者失败都会调用
        }
    })
```

### 关闭当前页，跳转到非tabbar页面的某页

``` js
    wx.redirectTo({
        url, // 页面路由
        success: () => {
            // 成功调用
        },
        fail: () => {
            // 失败调用
        },
        complete: () => {
            // 成功或者失败都会调用
        }
    })
```

### 关闭所有页面，打开某个页面
``` js
    wx.reLaunch({
        url, // 页面路由
        success: () => {
            // 成功
        },
        fail: () => {
            // 失败调用
        },
        complete: () => {
            // 成功失败都会调用
        }
    })
```