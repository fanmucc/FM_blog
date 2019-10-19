#### 固定样式打印
> 确定打印内容的宽高,设置合适的外边距,然后一遍一遍的查看效果,直到最佳为止;

不干胶、吊牌、洗唛等内容,一般情况下都是固定宽高,内容展示在具体的宽高中;

![吊牌](https://i.loli.net/2019/09/15/mtZDS3LG4Olh8db.png)
![不干胶](https://i.loli.net/2019/09/15/QVh61TmR9IycdXY.png)

##### 样式调配方法:
- 确定打印内容的宽高, 这里通过mm 毫米为单位进行确认;
- 调整外边距,让其在多张连续打印时外边距不会发生变化;
- 合理布局打印内容;

!> 连续多张打印是固定样式打印的痛点,需要通过大量的测试才能找到最优的外边距距离;

##### 调整外边距原因:
- 打印材料的纸张并不是百分百无缝连接的,它们一般具有一定的间距来让打印设备更好的确认是否已经走完一份内容(或者一张); 
- 如果按照无缝间距进行设置打印样式,单张打印是没有问题的,但是进行多张打印时,内容就是出现一份内容出现在两张打印材料上(错行打印);

![错误示例](https://i.loli.net/2019/09/15/j5ykpNWFeigoP8C.jpg)

##### 下面以蜜蜂系统的用户账号密码打印为例:

```HTML
<div class="printDivs" v-for="item in data" style="width: 50mm; height: 35mm; margin-bottom: 20px; padding: 0.1px;">
    <p class="p" style="margin-top: 25px;"><span class="printSpan">姓名:</span><span>@{{item.org_name}}</span></p>
    <p class="p"><span class="printSpan">账号:</span><span>@{{item.account}}</span></p>
    <p class="p"><span class="printSpan">密码:</span><span>@{{item.password}}</span></p>
</div>
```
![账号密码打印展示](https://i.loli.net/2019/09/15/6DnJF3jZdyGAbqM.png)

##### 这样设置理由:
- 不干胶打印纸宽度为50毫米,高度40毫米;
- 设置高度为35毫米,下边距为20px是为了保证兼容间距,让其多张打印的时候内容不走形(不出现一份内容跑到两张不干胶纸上)
- 设置p标签上边距让打印内容更好看;

图解:
![样式简介](https://i.loli.net/2019/09/14/5Q4BldD1RFOepMa.png)