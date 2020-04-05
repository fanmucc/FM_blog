#### Flex

> `Flex` 是 `Flexible Box` 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性,任何一个容器都可以指定为 Flex 布局。


6个容器属性:
``` css
flex-direction
flex-wrap
flex-flow
justify-content
aligin-items
align-content
```

### flex-direction
- 决定主轴的方向， 有4个值 `row`,`row-reverse`,`column`,`column-reverse`

1. `row`: 默认值, 主轴为水平方向，从左向右布局
2. `row-reverse`: 主轴为水平方向，从右向左布局
3. `column`: 主轴为垂直方向，从上到下布局
4. `column-reverse`: 主轴为垂直方向, 从下到上布局

<iframe height="265" style="width: 100%;" scrolling="no" title="qBdzmQX" src="https://codepen.io/fanmu/embed/qBdzmQX?height=265&theme-id=light&default-tab=html,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/fanmu/pen/qBdzmQX'>qBdzmQX</a> by fanmucc
  (<a href='https://codepen.io/fanmu'>@fanmu</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

### flex-wrap
- 默认情况下，项目都排在一条线（又称"轴线"）上。`flex-wrap`属性定义，如果一条轴线排不下，如何换行

1. `nowrap`: 默认值, 不换行
2. `wrap`: 换行, 第一行在上方
3. `wrap-reverse`: 换行, 第一行在下方

<iframe height="265" style="width: 100%;" scrolling="no" title="dyoBWEd" src="https://codepen.io/fanmu/embed/dyoBWEd?height=265&theme-id=light&default-tab=html,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/fanmu/pen/dyoBWEd'>dyoBWEd</a> by fanmucc
  (<a href='https://codepen.io/fanmu'>@fanmu</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

### flex-flow
> `flex-flow` 是`flex-direction`和`flex-wrap`的简写形势, 默认值为`row nowrap`

``` css
.box {
    flex-flow: <flex-direction> || <flex-wrap>
}
```

### justify-content
> `justify-content`属性定义了项目在主轴的上的对齐方式, 只对`row row-reverse`主轴设置方向有效

1. `flex-start`: 默认值, 主轴开始方向对齐, 此对齐方法首主轴方向影响`flex-direction`
2. `flex-end`: 主轴结束方向对齐, 此对齐方法首主轴方向影响`flex-direction`
3. `center`: 居中
4. `space-between`: 两端对齐, 项目之间的间隔相等
5. `space-around`: 每个项目两侧间隔相等, 项目之间的间隔比项目与边框的间隔大一倍

<iframe height="265" style="width: 100%;" scrolling="no" title="qBdzjOx" src="https://codepen.io/fanmu/embed/qBdzjOx?height=265&theme-id=light&default-tab=html,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/fanmu/pen/qBdzjOx'>qBdzjOx</a> by fanmucc
  (<a href='https://codepen.io/fanmu'>@fanmu</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

### align-items
> `align-items`属性定义项目在交叉轴上如何对齐, 受主轴方向影响`flex-direction: row OR column`

1. `stretch`: 默认值，默认设置`auto` 占满整个容器的高度
2. `flex-start`: 交叉轴的起点对齐
3. `flex-end`: 交叉轴的终点对齐
4. `center`: 居中
5. `baseline`: 第一行文字的基点对齐

<iframe height="265" style="width: 100%;" scrolling="no" title="yLNdXKM" src="https://codepen.io/fanmu/embed/yLNdXKM?height=265&theme-id=light&default-tab=html,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/fanmu/pen/yLNdXKM'>yLNdXKM</a> by fanmucc
  (<a href='https://codepen.io/fanmu'>@fanmu</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


### align-content
>`align-content`属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用

1. `flex-start`
2. `flex-end`
3. `center`
4. `space-between`
5. `space-around`

<iframe height="265" style="width: 100%;" scrolling="no" title="rNVEzJo" src="https://codepen.io/fanmu/embed/rNVEzJo?height=265&theme-id=light&default-tab=css,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/fanmu/pen/rNVEzJo'>rNVEzJo</a> by fanmucc
  (<a href='https://codepen.io/fanmu'>@fanmu</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

6个项目属性
``` css
order
flex-grow
flex-shrink
flex-basis
flex
align-self
```

### order
> `order`属性定义项目的排列顺序。数值越小，排列越靠前，默认为0

<iframe height="265" style="width: 100%;" scrolling="no" title="rNVEzrR" src="https://codepen.io/fanmu/embed/rNVEzrR?height=265&theme-id=light&default-tab=css,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/fanmu/pen/rNVEzrR'>rNVEzrR</a> by fanmucc
  (<a href='https://codepen.io/fanmu'>@fanmu</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

### flex-grow
> `flex-grow`属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。放大的前提条件是有空间；

<iframe height="265" style="width: 100%;" scrolling="no" title="abOgyRe" src="https://codepen.io/fanmu/embed/abOgyRe?height=265&theme-id=light&default-tab=css,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/fanmu/pen/abOgyRe'>abOgyRe</a> by fanmucc
  (<a href='https://codepen.io/fanmu'>@fanmu</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

### flex-shrink
> `flex-shrink`属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小， 当所有元素宽度大于父元素时次属性生效，`0`按照设置的宽度展示，`1`表示按照`flex`属性设置的值(平均值)进行展示，`2`表示按照平均值的2/1显示；

<iframe height="265" style="width: 100%;" scrolling="no" title="ExjBvGq" src="https://codepen.io/fanmu/embed/ExjBvGq?height=265&theme-id=light&default-tab=css,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/fanmu/pen/ExjBvGq'>ExjBvGq</a> by fanmucc
  (<a href='https://codepen.io/fanmu'>@fanmu</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

### flex-basis
> `flex-basis`属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。

<iframe height="265" style="width: 100%;" scrolling="no" title="GRJbvem" src="https://codepen.io/fanmu/embed/GRJbvem?height=265&theme-id=light&default-tab=css,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/fanmu/pen/GRJbvem'>GRJbvem</a> by fanmucc
  (<a href='https://codepen.io/fanmu'>@fanmu</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

### flex
> `flex`属性是`flex-grow`, `flex-shrink` 和 `flex-basis`的简写，默认值为`0 1 auto`。后两个属性可选。

``` css
.box {
    flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
```

### flex-self
> `flex-self`属性允许单个项目有与其他项目不一样的对齐方式，可覆盖`align-items`属性。默认值为`auto`，表示继承父元素的`align-items`属性，如果没有父元素，则等同于`stretch`。

1. `auto`
2. `flex-start`
3. `flex-end`
4. `center`
5. `baseline`
6. `stretch`

![flex-self](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071016.png)