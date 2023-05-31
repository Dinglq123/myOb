[掘金 flex布局](https://juejin.cn/post/7004622232378966046)
# 容器属性
## flex-direction 主轴方向
- row 水平
- row-reverse 水平反向
- column 竖直
- columen-reverse 竖直反向
## flex-wrap 是否换行
- no-wrap 不换行
- wrap 换行
- wrap-reverse 从反向换行
## juetify-content 元素在主轴方向的对齐方式
- flex-start 开始方向
- flex-end 结束方向
- center 居中
- space-between 两端对齐
- space-around 环绕对齐
## align-items 元素在交叉轴方向的对齐方式
- stretch 如果元素没有设置高度或者设为auto 将会占满整个容器的高度
- flex-start 上边对齐
- felx-end 下边对齐
- center 中心对齐
- baseline 以元素的第一行文字的极限对齐
## align-content 多个行在交叉轴方向的对齐
- flex-start 
- flex-end
- center
- space-between
- space-around
# 子元素属性
## order 
定义项目的排列顺序。数值越小，排列越靠前，默认为0
```css
.item {
    order: <integer>;
}
```
## flex-grow
定义项目的放大比例，**默认为0**，即如果**存在剩余空间时也不放大**。
这个系数是用来**分配剩余空间**的比例，而不是最终元素所占有空间的比例。
## flex-shrink
定义项目的缩小比例，**默认为1**，即**如果空间不足时，项目将缩小**。不能设置为负值。
空间不足时，将按照系数作为比例进行缩小。
## flex-basis
定义在**分配多余空间之前，项目占据的主轴空间**，浏览器会根据这个属性计算主轴是否有多余空间。默认值是auto，即项目本来的大小。
```css
.item {
    flex-basis: <length> | auto;
}
```
当主轴设置为水平时，当设置了 flex-basis，设置的项目宽度值会失效，flex-basis 需要跟 flex-grow 和 flex-shrink 配合使用才能生效。有两种特殊的值：
- 当 flex-basis 值为 0 % 时，项目尺寸会被认为是0，因此无论项目尺寸设置多少都用；
- 当 flex-basis 值为 auto 时，则跟根据尺寸的设定值来设置大小。
