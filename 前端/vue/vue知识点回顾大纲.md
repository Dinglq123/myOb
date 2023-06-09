# 回顾
* 插值和数据绑定
* 为什么使用this关键字访问data定义的属性?
* 动态绑定style 和class的区别？
  总的来说，`style` 绑定和 `class` 绑定都可以用于动态地设置元素的样式，但它们有不同的用途。如果您需要动态地设置元素的具体样式属性（例如文本颜色或字体大小），则应该使用 `style` 绑定。如果您需要根据某些条件动态地添加或删除 CSS 类，则应该使用 `class` 绑定。


vue中使用push,pop改变数组和使用fliter重写数组，对数组包含依赖的dom元素有什么影响?
	在Vue中使用`push`和`pop`方法改变数组是直接修改原数组的操作，而使用`filter`则是返回一个新的数组。因此，它们对包含依赖的DOM元素的影响是不同的。
	当使用`push`或`pop`方法改变数组时，Vue会检测到数据变化并重新渲染相关的DOM元素。这是因为Vue通过劫持数组的方法来监听数据变化，从而能够及时更新DOM元素。
	而使用`filter`方法重写数组则会返回一个新的数组，这个新数组和原来的数组不再是同一个对象。因此，Vue无法直接检测到数据的变化，也就无法自动更新相关的DOM元素。在这种情况下，你需要手动触发Vue的更新机制，即使用`$forceUpdate`方法来强制更新组件。
	需要注意的是，虽然使用`filter`方法重写数组会导致Vue无法自动检测到数据变化，但是如果你将新数组赋值给原数组，即`this.array = this.array.filter(...)`，Vue仍然能够检测到数据变化并自动更新相关的DOM元素。这是因为赋值操作会触发Vue的响应式机制。
`v-model`和`refs`在绑定number类型的数据时有什么区别：
	`v-model`会自动的把数据类型转化为数字类型
	`refs`或者java原生的方式会默认使用字符串的类型。