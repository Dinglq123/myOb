# 文件组织结构
## main.js
## App.vue
## components/FriendContact.vue

# 大纲
![[Pasted image 20230306205852.png]]
# 常用命令

```html
// html访问js中的变量
{{name}}    //在成对的符号中间 用法名称：“插值” interpolation

v-bind:value='func'   //重新绑定属性,右侧是字符串形式的java表达式。
	v-bind:value="func"
	v-bind:value="func()"
	v-bind:value="func(5)"

v-html=      //代码被解释为html代码
  <p v-html="outputGoal()" v-bind:title="message"></p>

<input v-model="message"></input>  //双向绑定，背后是两个操作：1.v-on绑定input事件传递到函数中。2.函数会返回的值赋值到绑定的属性中

<p v-once>Staring counter: {{ counter }}</p>   ////不更新，只绑定一次

//表单： 点击按钮会提交表单，自动刷新页面
<form @submit.prevent="myfun">  //阻止默认的刷新方法，并调用myfun()

// :disabled:禁用按钮
  <button

	:disabled="mayUseSpecialAttack"

	@click="specialAttackMonster"

	title="Can use every third round"

  >

	Special Attack

  </button>


//部件向主程序发送消息
this.$emit("event-name");

//  常用的监听事件
v-once  //不更新，只绑定一次
v-on:click  //鼠标左击
@click.right  //鼠标右击
@input  //键盘输入
@keyup  //键盘输入
@keyup.enter  //键盘输入 【enter】键







const app=Vue.createApp({

  data(){
    return {
      counter:0,
      name:'dingleqi',
      final_name:''
    };
  },
  watch:{
  // 观察者，同名函数会在同名属性被更新时调用
  name(value， old_value){//  用于在self.name属性改变时，调用。value参数自动获取name的最新的值,old_value参数为上一次的值，可选。
  } 	  
  },
  computed:{
  
  //  计算，当函数所依赖的值被更新时，会调用有依赖关系的函数。必须要返回一个值。  
  //  当成属性一样使用，不用加括号，不能被事件触发
  },
  methods:{

  }

});
// 使用css的id选择器选择events
app.mount("#events")


```
`v-show`和`v-if`
v-show显示或者隐藏元素，v-if删除或者添加元素。
当元素比较多的时候，使用v-show。当元素比较少的时候使用v-if。
```html
v-if和v-else  //一个 `v-else` 元素必须跟在一个 `v-if` 或者 `v-else-if` 元素后面，否则它将不会被识别。
      <p v-if="goals.length === 0">
        No goals have been added yet - please start adding some!
      </p>

      <ul v-else>
      </ul>
v-show 显示或者隐藏
      <p v-show="goals.length === 0">
        No goals have been added yet - please start adding some!
      </p>

      <ul v-show="goals.length > 0">
      </ul>
```
`v-for`
必须要使用`key`关键字，不然在删除元素的时候会因为**vue重用dom元素**而出现bug。
具体解释：
Vue 默认按照“就地更新”的策略来更新通过 `v-for` 渲染的元素列表。当数据项的顺序改变时，Vue 不会随之移动 DOM 元素的顺序，而是就地更新每个元素，确保它们在原本指定的索引位置上渲染。
默认模式是高效的，但**只适用于列表渲染输出的结果不依赖子组件状态或者临时 DOM 状态 (例如表单输入值) 的情况**。
```html
        <li

          v-for="(goal, index) in goals"

          :key="goal"  //goal只能在<li></li>里面访问

          @click="removeGoal(index)"

        >

          <p>{{ index+1 }} - {{ goal }}</p>

          <!-- .stop stops propagation (bubbling), doesnt trigger outer events -->

          <input type="text" @click.stop />

        </li>
```


函数不适合绑定输出动态的值，因为vue中有一个值被更新时，会重新调用所有的函数
conputed属性会在依赖项发生变化时，重新加载。不能被事件触发
# Vue的核心
## Interpolation and data binding
插值：`<p>{{ outputGoal() }}</p>`
	在成对的符号中间，里面写js表达式。
绑定:`<a :href="vueLink">Vue website</a>`=`<a v-bind:href="vueLink">Vue website</a>`
	绑定html元素的某个属性，使用引号，里面写js表达式。
## 使用this关键字访问data属性？
createApp()会返回一个实例，这个实例整合了data、methods等里面所有的属性。


# Vue原则
## `data`
一个function，返回一个对象。可以使用缩写的方式：`data(){return{messageA:"",messageB:""};}`

## `methods`
一个对象。对象里面都是函数。`methods:{funcA():{}}`
**主要用于事件绑定 或者 需要时时更新的变量**
可以绑定到事件，插值使用。
当vue中有任何一个变量更新时，里面的函数都会被调用一次。

### 函数调用的方式：
初级版本：基本写死，调用函数的参数和按钮是绑定的，事件不会返回需要的信息。
使用部件:button
```javascript
// 定义：
increment(num=1) {
  this.counter += num;
}
// 调用：
<button v-on:click="increment">Add</button>
<button v-on:click="increment(1)">Add</button>
<button @click="increment(10)">Add 10</button>

```
高级版本：函数的执行需要使用到事件返回的信息。
使用部件：input
JavaScript触发事件的时候会返回一个事件对象`event`，在函数定义中可以使用`event.target.props`访问元素的属性。
使用一：
```javascript
//定义
setName(event, lastName) {
	this.name = `${event.target.value} ${lastName}`;
},
//调用
  <input
	type="text"
	@input="setName($event, 'Osrečki')"
  />
```
使用二：
如果写`@input="setName"`,会自动把这个事件对象进行传入。
```
//定义
setName(event) {
	this.name = event.target.value;
},
//调用
  <input
	type="text"
	@input="setName"
  />
```
总结：
* 首先如果html 中直接使用函数名，而不是函数调用，事件的对象会作为第一个参数传入。
* 如果想要使用函数调用并且使用事件作为参数，可以使用`$event`来访问内置的默认对象，例如：`@input="setName($event, 'Osrečki')"`


## `computed`
**用于依赖于其他变量的变量**
***必须有返回值，像data里面定义的变量一样使用，计算属性里面不能嵌套计算属性***
***不能在计算属性中修改data里面的值***
对于计算属性有依赖的data变化时，调用依赖的函数。
为什么不是用函数调用来实现？
**答：计算属性基于响应式依赖存储，只有在响应式依赖更新时才重新计算。而方法调用总是在重渲染发生时再次执行函数。**
```javascript
  computed: {

    fullname() {

      console.log('Running output full name');

      if (this.name == '' && this.lastName == '') {

        return '';

      }

      return `${this.name} ${this.lastName}`;

    },

    computedTime() {

      const now = new Date();

      const hours = now.getHours();

      const minutes = now.getMinutes();

      const seconds =

        now.getSeconds() < 10

          ? '0' + now.getSeconds()

          : now.getSeconds();

      const ms = now.getMilliseconds();

      const time = `${hours}:${minutes}:${seconds}:${ms}`;

      return time;

    },

  },
```

## `watch`
**主要用于防止不希望的数据改变，比如显示时间，时间具有边界**
***函数名为同名属性***
```javascript
  watch: {

    counter(value) {

      if (value > 50 || value < 0) {

        this.counter = 0;

      }

    },

    name(newValue, oldValue) {

      console.log('first');

      if (newValue == '') {

        this.fullname = '';

      } else {

        this.fullname = newValue + ' ' + this.lastName;

      }

    },
  },
```
## `props`
用于主程序向部件传递信息。
***Props的值在部件中不可以被修改，如果想实现修改的效果，可以在用props的值初始化data的一个属性，并修改利用data的值***
```vue
部件与主程序之间的通信
//部件中的props属性，用于主程序向部件中传递消息

数组形式，需要加双引号：
// props: ["name", "phoneNumber", "emailAddress","isFavorite"],
// 字典的两种形式
props:{

name:String,

phoneNumber:{

  type:String,

  required:true

},

emailAddress:String,
// 使用默认值
isFavorite:{

  type:String,

  required:false,

  default:'0'

}

},
  
 //主程序中使用v-bind来向props属性传递形参
  <friend-contact

	v-for="friend in friends"

	:key="friend.id"

	:id="friend.id"

	:name="friend.name"

	:phone-number="friend.phone"

	:email-address="friend.email"

	:is-favorite="friend.isFavorite"

></friend-contact>

// 使用props来初始化data属性：
  props: ["name", "phoneNumber", "emailAddress","isFavorite"],

  data() {

    return {

      detailsAreVisible: false,

      favoriteTag:this.isFavorite,

    };

  },

```
## `emits`
用于标识部件向主程序传递的事件。
```JavaScript
//定义：这是为了工程化，让别人能清楚我们这个组件会触发哪些事件
emits: ['toggle-favorite', 'delete'],
// emits:['toggle-favorite'],

  emits:{
    'toggle-favorite':function(id){
      if(id){
        return true;
      }else{
        console.warn('Id is missing!');
        return false;
      }
    }
  },
//使用1：
<button @click="$emit('delete', this.id)">Delete</button>

//使用2：
    toggleFavorite() {

      // emit our custom events, defina arguments which are passed in when event cought

      this.$emit('toggle-favorite', this.id);

    },
```
## `provide`和`inject`
用于包含的部件关系中，跨层传递信息
尽量少使用
```JavaScript
// 主部件中：
provide:{

}
// 子部件调用：
inject：[]
```
## `<style scoped>`
作用：使css只作用于当前的组件（模板）
底层实现：给组件和选择器加上特殊的代码
```JavaScript
<style scoped>

  header {

    width: 100%;

    height: 5rem;

    display: flex;

    justify-content: center;

    align-items: center;

    background-color: #14005e;

  }

  

  header h1 {

    color: white;

    margin: 0;

  }

</style>
```
## v-model
[v-mode的使用](https://cn.vuejs.org/guide/components/v-model.html#handling-v-model-modifiers)
## 类和样式绑定
可以传入一个对象、数组进行绑定。
```html
data() {
  return {
    isActive: true,
    hasError: false
  }
}

<div
  class="static"
  :class="{ active: isActive, 'text-danger': hasError }"
></div>


```

##  `<slot></slot>`
[[slot]]

总的来说，`slot` 是 Vue 组件中非常重要的一个特性，可以让组件更加灵活和可复用。

作用：
可以把代码拆分为多个部件，*用于自定义一个样式，可以往里面动态地放html代码*。这个用法介于全局样式和`<style scoped>`之间，比如说我需要一个圆角的卡片，里面可以放组件，就可以定义一个`slot`。
同时在一个卡片里也能定义多个`slot`，可以实现把html代码拆分放入到多个slot里面（没有指定`slot`的全部放在默认的`slot`里面）
* 只能有一个默认的slot，如果有不止一个slot，需要用name来区分.`<slot name=header></slot>`
* 如果有多个slot，使用`<template #header></template>`或者`<template v-slot:header></template>`来指定slot
* slot可以向调用的模板中传递数据:slot中的定义：`<slot :task='task' deadline='ddl'>`***注意第二个没有冒号***。使用：`<template #default='taskitem'></templete>`此时taskitem是一个对象。
* ***部件中定义的`<style scoped>`，不会影响传递到slot中的那部分样式。***
### 定义带有slot的组件：
```JavaScript

<template>

<div>

  <header>

    <!-- 有名字的slot -->

    <slot name="header"></slot>

  </header>

  <!-- 默认的slot,只能有一个 -->

  <slot></slot>

</div>

</template>

  

<script>

export default {

}

</script>

  
  
  

<style scoped>

div {

  margin: 2rem auto;

  max-width: 30rem;

  border-radius: 12px;

  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);

  padding: 1rem;

}

</style>



```
### 调用：
```
<template>

  <section>

    <!-- 使用这个组件 -->

    <base-card>

    <!-- 指定使用header这个slot,里面的代码会被送到这个slot里面 -->

    <template #header>

      <h3>{{ fullName }}</h3>

      <base-badge :type="role" :caption="role.toUpperCase()"></base-badge>

    </template>

    <!-- 其余的代码都被送到默认的slot里面 -->

    <p>{{ infoText }}</p>

  </base-card>

  </section>

</template>
```
## 实例的生命周期
![[Pasted image 20221019152717.png]]
## Vue怎么更新dom
通过内存中的虚拟dom，当有data或者computed属性更新的时候，先创建一个新的虚拟Dom，然后和之前的做对比。如果不同就重新渲染浏览器的dom。
![[Pasted image 20230308100750.png]]

## 注册组件

### **全局组件**：在`main.js`中注册，全局都可以使用。
存在问题：
* 每个组件都包含`templete`和`style`，如果注册全局使用的话，浏览器在加载的时候需要直接下载所有组件的代码。
* 代码会很长。
* 有的组件只使用一次，有的频繁使用，应该区别对待。
``` JavaScript
import { createApp } from 'vue';

  

import App from './App.vue';

import TheHeader from './components/TheHeader.vue';

import BaseBadge from './components/BaseBadge.vue';

import BadgeList from './components/BadgeList.vue';

import UserInfo from './components/UserInfo.vue';

  

const app = createApp(App);

  

app.component('the-header', TheHeader);

app.component('base-badge', BaseBadge);

app.component('badge-list', BadgeList);

app.component('user-info', UserInfo);

  

app.mount('#app');
```

### **局部组件**，在`script`中注册，并使用`components:`
```JavaScript

<script>

// 引入部件

import TheHeader from './components/TheHeader.vue';

export default {

  // compoents属性 键值对： 部件名：部件对象

  components:{'the-header':TheHeader},

  data() {

    return {

      activeUser: {

        name: 'Maximilian Schwarzmüller',

        description: 'Site owner and admin',

        role: 'admin',

      },

    };

  },

};

</script>
```

### 动态组件
[[动态组件]]
* `<component :is="component-name"></component`，可以设置一个data属性，组件的名字。***好处是***相较于`v-if`判断是否展示某个组件，这样写更短，并且不会有空的dom元素。***缺点是***切换的时候原来的dom元素会被销毁，导致信息丢失，比如`<input>`里面的信息。
* `<keep-alive></keep-alive>`用于解决上述的缺点，告诉vue，不要销毁其中的部件。同样适用于`v-if`的实现方式。
* 如果使用动态组件代替`v-if`模式，则会搭配`provide`和`inject`，`TheResource.vue->StoredResources.vue/AddResource.vue`，因为动态组件不能动态绑定。


### `<teleport to="body"></teleport>`
改变dom元素的层级，比如把警告的窗口放到body一层子节点的底部，而不是在一个很深的嵌套里面。组织合理的html结构。
Vue 的 teleport 是一个渲染内容到其他 DOM 节点的组件。它可以在 DOM 树中的任何位置渲染一个组件，并且可以在该组件的父组件之外进行渲染。
通常，当您需要将组件渲染到一个与组件层次结构不同的 DOM 元素中时，可以使用 teleport。例如，您可能希望将弹出窗口渲染到页面的顶部，而不是作为组件的子项。
要使用 teleport，您需要使用 <teleport> 元素将需要渲染的组件包装起来，并将 to 属性设置为一个 CSS 选择器，该选择器指向要将组件渲染到的 DOM 元素。

## 学习错误记录
* 传出字典格式的配置信息时，可变的都放在右边，不要返回一个可变的键
* method中引用data中的数据都需要使用`this`指针
* `v-for="goal in goals"`这个语法可以访问对象中的元素，同时也可以添加`index`参数：`（goal，index) in goals`有一个原则是：***优先访问的放在前面，例如列表中：元素>索引  字典中： 值>键>索引***。`:key=""`关键字用于区分不同的dom对象，防止Vue自身优化进制（Vue会重用dom元素）产生错误。
* `@click="func('msg')"`传递进去的字符串需要用单引号！

