## Vue 的 `slot` 是用来在组件中承载内容的一个特殊标签。使用 `slot`，可以让组件更加灵活，具有更高的可复用性和组合性。

具体来说，`slot` 可以实现以下几个功能：

1.  插槽内容的默认值：在组件的模板中，可以使用 `slot` 标签来定义一个或多个插槽。当组件被使用时，如果没有传入任何内容到插槽中，那么默认情况下会显示 `slot` 标签中的内容。
    
2.  具名插槽：有时候，一个组件需要承载多个不同的内容。使用 `slot` 的具名插槽，可以定义多个插槽，并为每个插槽起一个名称。这样，在组件被使用时，可以根据插槽的名称来决定插入哪个内容。
    
3.  作用域插槽：有时候，一个组件需要将一些数据传递给插槽中的内容。使用作用域插槽，可以在插槽内部使用组件的数据，并将数据传递给插槽的内容。这样，可以让插槽更加灵活，可以根据需要来显示不同的内容。
    
下面分别举例说明 `slot` 的三个功能：

1.  插槽内容的默认值：

在一个 `card` 组件中，可能需要承载一些标题、文本和图片等内容。可以使用 `slot` 定义一个默认插槽，当组件被使用时，如果没有传入任何内容到插槽中，那么默认情况下会显示 `slot` 标签中的内容。

```vue
<template>
  <div class="card">
    <div class="card-header">
      <slot name="header">
        <h3>Default Header</h3>
      </slot>
    </div>
    <div class="card-body">
      <slot></slot>
    </div>
  </div>
</template>

```

在使用 `card` 组件时，可以选择传入自己的标题和内容：
```vue
<template>
  <div>
    <card>
      <template #header>
        <h3>Custom Header</h3>
      </template>
      <p>Custom Content</p>
    </card>
  </div>
</template>

```

2.  具名插槽：

在一个 `modal` 组件中，可能需要承载多个按钮，如确认按钮和取消按钮。可以使用 `slot` 定义多个具名插槽，并为每个插槽起一个名称。这样，在组件被使用时，可以根据插槽的名称来决定插入哪个按钮。

```vue
<template>
  <div class="modal">
    <div class="modal-header">
      <slot name="header">
        <h3>Default Header</h3>
      </slot>
    </div>
    <div class="modal-body">
      <slot></slot>
    </div>
    <div class="modal-footer">
      <slot name="footer">
        <button @click="close">Close</button>
      </slot>
    </div>
  </div>
</template>

```
在使用 `modal` 组件时，可以选择传入自己的按钮：

```vue
<template>
  <div>
    <modal>
      <template #header>
        <h3>Custom Header</h3>
      </template>
      <p>Custom Content</p>
      <template #footer>
        <button @click="save">Save</button>
        <button @click="cancel">Cancel</button>
      </template>
    </modal>
  </div>
</template>

```

3.  作用域插槽：

在一个 `list` 组件中，需要承载多个列表项。每个列表项包含一个标题和一些文本。可以使用作用域插槽，将组件的数据传递给插槽的内容，使得每个列表项可以显示不同的标题和文本。
```vue
<template>
  <div class="list">
    <div class="list-item" v-for="item in items" :key="item.id">
      <slot :item="item">
        <h3>{{ item.title }}</h3>
        <p>{{ item.text }}</p>
      </slot>
    </div>
  </div>
</template>

```

在使用 `list` 组件时，可以自定义每个列表项的标题和文本

## `slot`+`v-show`容易出错！

当使用 `v-show` 控制包含 `slot` 的组件的显示时，其表现与控制普通元素的显示是不同的。因为 `slot` 插槽可以让子组件在父组件中动态地渲染内容，所以控制包含 `slot` 的组件的显示会比较复杂，会有以下两种情况：
```vue
<template>
  <div>
    <h2>这是标题</h2>
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: 'MyComponent',
  data() {
    return {
      show: true
    }
  }
}
</script>

```

1.  当 `v-show` 直接作用于包含 `slot` 的组件时，只有该组件的顶层元素会受到 `v-show` 的影响，而 `slot` 中的内容不受影响。也就是说，如果使用 `v-show` 控制包含 `slot` 的组件的显示时，只有组件的外层包裹元素会根据 `v-show` 控制显示或隐藏，而插入到 `slot` 中的内容会一直存在于 DOM 中。
```vue
<my-component v-show="show"></my-component>

```
那么当 `show` 为 `false` 时，该组件会隐藏 `div` 和其中的内容（即标题和插槽），而其它部分不受影响。
    
2.  当 `v-show` 作用于包含 `slot` 的子组件时，该子组件及其插槽内容都会受到 `v-show` 的影响，即可以通过控制子组件的显示来同时控制插入到插槽中的内容的显示。在这种情况下，子组件的渲染将由 `v-show` 控制，因此整个组件会被渲染或隐藏。
```vue
<div v-show="show">
  <my-component></my-component>
</div>

```
如果将 `v-show` 绑定在包含整个组件的元素上,那么当 `show` 为 `false` 时，整个组件都会被隐藏。
## `slot`+`v-if`没有上述问题