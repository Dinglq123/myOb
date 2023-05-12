## Vue权限管理
Vue 的权限管理通常可以分为两个层次：路由级别和按钮级别。
### 1.路由级别
路由级别的权限管理通常是指在路由跳转前校验用户是否有访问该页面的权限。我们可以通过 Vue Router 的导航守卫 beforeEach 进行处理。在每次路由跳转前，都会触发 beforeEach，我们可以在该钩子函数中根据当前用户的角色信息进行判断，如果用户有权限访问该路由，则放行；否则跳转到无权限页面或其他需要登录的页面。例如：
```js
router.beforeEach((to, from, next) => {
  const loggedIn = localStorage.getItem('token')
  if (to.matched.some(record => record.meta.requiresAuth)) {
    // 需要登录才能访问的页面
    if (!loggedIn) {
      next('/login')
      return
    }
  }
  
  if (to.matched.some(record => record.meta.requiresAdmin)) {
    // 需要管理员权限才能访问的页面
    if (!checkAdminRole()) {
      next('/no-permission')
      return
    }
  }

  next()
})

```
在上述代码中，beforeEach 判断了所访问的页面是否需要登录或需要管理员权限，并根据当前用户是否具有权限进行跳转。

### 2.按钮级别
按钮级别的权限管理通常是指在渲染页面时，根据用户的角色信息控制某些按钮是否显示。我们可以在组件中使用 v-if 或者 v-show 根据当前用户的角色信息来控制按钮的显示与隐藏。例如：
```js
<button v-if="isAdmin">管理员操作</button>
```
在上述代码中，v-if 根据该组件所对应的数据 isAdmin 判断当前用户是否为管理员，如果是，则显示该按钮。
总之，路由级别和按钮级别的权限管理可以相互结合使用，根据不同的场景进行处理，以保证系统的安全性。
### Vue父组件嵌套了子组件，生命周期函数怎么执行？
在 Vue 中，一个父组件嵌套了子组件时，它们之间的生命周期函数顺序如下：
1. 父组件 beforeCreate 钩子函数
2. 父组件 created 钩子函数
3. 父组件 beforeMount 钩子函数
4. 子组件 beforeCreate 钩子函数
5. 子组件 created 钩子函数
6. 子组件 beforeMount 钩子函数
7. 子组件 mounted 钩子函数
8. 父组件 mounted 钩子函数

对于更新来说生命周期函数的执行顺序是：
1. 父组件 beforeUpdate 钩子函数
2. 子组件 beforeUpdate 钩子函数
3. 子组件 updated 钩子函数
4. 父组件 updated 钩子函数

如果组件被销毁，钩子函数的执行顺序为：
1. 父组件 beforeDestroy 钩子函数
2. 子组件 beforeDestroy 钩子函数
3. 子组件 destroyed 钩子函数
4. 父组件 destroyed 钩子函数

从上述生命周期函数的执行顺序可以看出，在组件渲染过程中，父组件的生命周期函数总是在子组件之前执行；而在组件更新过程中，先执行父组件的 beforeUpdate 钩子函数，再依次执行子组件的 beforeUpdate 和 updated 钩子函数，最后执行父组件的 updated 钩子函数。