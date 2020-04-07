#### 生命周期

### Page页面

``` js
page({
    onLoad () {
        // 监听页面加载
    },
    onReady () {
        // 监听页面初次渲染完成，只会触发一次
    },
    onShow () {
        // 监听页面显示
    },
    onHide () {
        // 监听页面隐藏
    },
    onUnload () {
        // 监听页面卸载
    },
    onPullDownRefresh () {
        // 今天用户下拉动作
    },
    onReachBotton () {
        // 用户上拉触底事件
    },
    onShareAppMessage () {
        // 用户触发右上角转发按钮
    },
    onPageScroll () {
        // 页面滚动触发事件处理函数
    },
    onTabItemTap () {
        // 单签是tab页面时， 点击tab时触发
    }
})
```

### Component组件
``` js
Components({
    properties: {
        // 接收的默认参数
    },
    lifetimes: {
        created () {
            // 组件初始化
        },
        attached () {
            // 组件初始化完成
        },
        ready () {
            // 组件在视图层布局完成
        },
        moved () {
            // 组件实例被移动到节点树的另一个位置执行
        },
        detached () {
            // 组件实例从页面节点移除事执行
        },
        error (err) {
            // 组件方法抛出错误时执行
        }
    },
    // 组件在页面中的生命周期
    pageLifetimes: {
        show () {
            // 页面展示
        },
        hide () {
            // 页面隐藏
        },
        resize () {
            // 页面尺寸发生变化
        }
    }
})
```