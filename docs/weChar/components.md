#### 小程序常用组件

### view

视图容器

``` wxml
<view hover-class="" hover-stop-propagation="false" hover-start-time="50" hover-stay-time="400"></view>
```
视图容器的可选属性
- `hover-class`: 用户按下去的样式名，点击效果。 class名
- `hover-start-time`: 设置时间，用户点击后多久出现点击效果。 Number
- `hover-stay-time`: 用户手指离开后多久，点击效果消失。 Number
- `hover-stop-propagation`: 是否阻止本节点的祖先出现点击状态。Boolean

### scroll-view

可滚动的的视图区域 [scroll-view详细文档](https://developers.weixin.qq.com/miniprogram/dev/component/scroll-view.html)

```
<scroll-view scroll-x="false" scroll-y="false" upper-threshold="50" lower-threshold="50" bindscrolltoupper="" bindscrolltolower="">
    滚动的内容
</scroll-view>
```

可滚动的视图区域，其中几个属性，具体可以查看scroll-view文档

- `scroll-x/scroll-y`: 滚动方向. Boolean
- `upper-threshold`: 距离顶部(scorll-y)或者左侧(scroll-x)多少距离时，如果到了此距离会触发`bindscrolltoupper`事件
- `lower-threshold`: 距离底部(scorll-y)或者右侧(scroll-x)多少距离时，如果到了此距离会触发`bindscrolltolower`事件

### swiper

滑块视图容器 [swiper详细文档](https://developers.weixin.qq.com/miniprogram/dev/component/swiper.html)

```
<swiper indicator-dots="{{indicatorDots}}" autoplay="{{autoplay}}" interval="{{interval}}" duration="{{duration}}">
    <block wx:for="{{background}}" wx:key="*this">
        <swiper-item>
            <view class="swiper-item {{item}}"></view>
        </swiper-item>
    </block>
</swiper>
```

部分属性
- `indicator-dots`: 是否显示面板指示点。 Boolean
- `autoplay`: 是否自动切换。 Boolean
- `interval`: 自动切换的事件。 Number
- `duration`: 滑块动画时长
- `block`: 为滑块内容区
- `swiper-item`: 放在内容区时，高度自动设置为100%;
