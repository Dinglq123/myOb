文本类型的变量，初始化为空字符串
数字类型的变量，初始化为`null`
`<select>\<select>`类型，初始化其中一个默认值。

多选框`        <input id="interest-news" name="interest" type="checkbox" vlaue="news" v-model="interest"/> <label for="interest-news">News</label>`
```vue
定义数据：
      interest: [],  使用数组存储勾选的状态值，被存储的是勾选组组件的value值

    <div class="form-control">
      <h2>What are you interested in?</h2>
      <div>
        <input
          id="interest-news" 和label搭配
          name="interest"  和多个input组件的name都必须一样，才能都保存到那个数组
          type="checkbox" 多选框的类型
          vlaue="news" 当被勾选时，保存到数组中的数值
          v-model="interest" 必须绑定同一个data属性数组
        />
        <label for="interest-news">News</label>
      </div>
      <div>
        <input
          id="interest-tutorials"
          name="interest"
          type="checkbox"
          value="tourials"
          v-model="interest"
        />
        <label for="interest-tutorials">Tutorials</label>
      </div>
      <div>
        <input
          id="interest-nothing"
          name="interest"
          type="checkbox"
          value="nothing"
          v-model="interest"
        />
        <label for="interest-nothing">Nothing</label>
      </div>
    </div>
 ```
单个确认框
单选框`<input id="how-video" type="radio" name="how" vuale="video" v-model="how"><\input>`
```html
数据的定义：how: "",定义为字符串，后面单选的组件的value会保存在这个data中
    <div class="form-control">
      <h2>How do you learn?</h2>
      <div>
        <input
          id="how-video"
          name="how"  保持一致
          type="radio" 
          vuale="video" 每个组件应该保持不同
          v-model="how" 绑定一个字符串
        />
        <label for="how-video">Video Courses</label>
      </div>
      <div>
        <input
          id="how-blogs"
          name="how"
          type="radio"
          value="blog"
          v-model="how"
        />
        <label for="how-blogs">Blogs</label>
      </div>
      <div>
        <input
          id="how-other"
          name="how"
          type="radio"
          value="other"
          v-model="how"
        />
        <label for="how-other">Other</label>
      </div>
    </div>
```



`v-model`和`refs`在绑定number类型的数据时有什么区别：
	`v-model`会自动的把数据类型转化为数字类型
	`refs`或者java原生的方式会默认使用字符串的类型。