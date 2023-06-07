# JS
## 数据类型
基础数据类型：Undefined、Null、Boolean、Number、String、Symbol【ES6】、Bigint【ES10】 
复杂数据类型（三大引用类型）：Object、Array、Function  【Arrar和Function都属于Object类型】
## 深拷贝和浅拷贝
浅拷贝就是可以将对象的基础类型复制，无法复制复杂数据类型
深拷贝就是为了解决无法复制复杂数据类型，对数据进行深程度拷贝
### 浅拷贝
Object.assign
```js
var obj1 = {
    name:'zangsan',
    age: 18
}
var obj2 = Object.assign(obj1);

console.log(obj1, obj2)
```
拓展运算符（...）
**可以用于扩展可迭代对象的元素，或者对象的属性（即键值对）**
```js
var obj1 = {
    name:'zangsan',
    age: 18
}
var obj2 = {...obj1};

console.log(obj1, obj2)
```
for ... in
```js
function copy(obj1) {
   var obj = Array.isArray(obj1) ? [] : {};
   for (let i in obj1) {
   obj[i] = obj1[i];
  }
   return obj;
}

var obj1 = {
    name:'zangsan',
    age: 18
}

var obj2 = copy(obj1);
console.log(obj1, obj2)
```
Object.create
```js
let clone = Object.create(
  Object.getPrototypeOf(obj),
  Object.getOwnPropertyDescriptors(obj)
);
```
### 深拷贝
JSON对象来实现深拷贝【缺点：函数无法拷贝，会显示undefined】
```js
var obj1 = {
    name:'zangsan',
    age: 18,
    hobby:{
        motion: new Array('篮球','足球'),
    }
}

function deepClone(obj) {
  var _obj = JSON.stringify(obj),
    objClone = JSON.parse(_obj);
  return objClone;
}

var obj2 = deepClone(obj1);
console.log(obj1, obj2);
```
lodash函数库实现深拷贝【需要引入lodash库】
```js
var obj1 = {
    name:'zangsan',
    age: 18,
    hobby:{
        motion: new Array('篮球','足球')
    }
}

var obj2 = _.cloneDeep(obj1);
console.log(obj1, obj2);
```
**递归**
```js
function deepClone(obj) {
  // 判断是否是对象或数组
  if (typeof obj !== "object" || obj === null) {
    return obj;
  }

  // 创建新的对象或数组
  const result = Array.isArray(obj) ? [] : {};

  // 递归拷贝子元素
  for (let key in obj) {
    const value = obj[key];
    result[key] = deepClone(value);
  }

  return result;
}

```
## 创建对象的方式
![[创建对象的方式#工厂模式]]
![[创建对象的方式#构造函数模式]]
![[创建对象的方式#原型模式]]
## 怎么判断某个属性是在实例上还是在其原型上？
![[创建对象的方式#^082b57]]
![[创建对象的方式#^rq712j]]
## 继承的几种实现方式
![[继承]]
## 改变函数作用域

![[前端/javascript/函数#^ff8528|函数]]
![[前端/javascript/函数#^c8ab15|函数]]
## 事件捕获和冒泡
- 捕获型事件：事件从document对象开始触发，然后到目标事件
- 冒泡型事件：目标事件到document对象的顺序触发。
## DOM操作
- onclick--------点击事件
- onload---------进入时执行事件
- onunload-------离开时执行事件
- onmouseover----鼠标指针移入时执行事件
- onmouseout-----鼠标指针移出时执行事件
- onmousedown----鼠标摁下时执行事件
- onmouseup------鼠标松开时执行事件
## AJAX
- AJAX是异步 JavaScript 和 XML。
- AJAX可以通过在后台与服务器进行少量数据交换,实现异步更新。
- AJAX的XmlHttpRequest使您可以使用JavaScript向服务器提出请求并处理响应，而不阻塞用户。
- AJAX通过XMLHttpRequest对象，Web开发人员可以在页面加载以后进行页面的局部更新。
- AJAX常用的方法：（新增）post,（获取）get,（删除）delete, （修改）put
- 原生AJAX请求
```js
//创建 XMLHttpRequest 对象
var ajax = new XMLHttpRequest();
//规定请求的类型、URL 以及是否异步处理请求。
ajax.open('GET',url,true);
//发送信息至服务器时内容编码类型
ajax.setRequestHeader("Content-type", "application/x-www-form-urlencoded"); 
//发送请求
ajax.send(null);  
//接受服务器响应数据
ajax.onreadystatechange = function () {};
```
## 宏任务和微任务
