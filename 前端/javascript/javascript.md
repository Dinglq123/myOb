# 基本概念
## 基础语法
### 数据类型
五种简单的数据类型+**Object**
* Undefined
* Null 
* Boolean
* Number
* String
* Object
--------
`typeof`操作符：检测给定变量的数据类型
![[Pasted image 20220922164133.png]]
#### Undefined
只有一个值，即`undefined`。使用`var`声明变量但没有初始化时，默认为undefined，同时对未声明的变量求typeof，即`typeof(undeclare_i)==undefined`
#### Null
只有一个值，即null。逻辑上表示一个空对象指针
#### Boolean
有两个值true或者false。与数字值不统一，true不一定等于1，false不一定等于0。
转换规则：
![[Pasted image 20220922165500.png]]
#### Number
##### 整数
0开头为8进制
0x开头为16进制
在进行数值计算的时候都被会转化为10进制
##### 浮点
*浮点数字即必须包含一个小数点，并且小数点后至少有一位数字*。
js会不失时机的把浮点类型的整数转化为整数。
![[Pasted image 20220922170728.png]]
超出数值范围会转化为`Infinity`或者`-Infinity`，可以使用`isFinite`来判断。
##### NaN
特殊的一个数值，适用于返回数值的函数不能返回数值的情形。
* `isNaN(NaN)==true`
* 任何与`NaN`相关的运算都返回`NaN`
* `NaN`与任何数值都不相等，包含`NaN`本身。
`isNaN()`用于返回参数是否"不是数值"。
![[Pasted image 20220922171714.png]]
##### 数值转换
三个函数
* `Number()`    可以用于任何数据类型
* `parseInt()`    把字符串转化为整数
* `parseFloat()`    把字符串转化为浮点数
-------
###### `Number()`
* 可以把字符串中的16进制识别出来，但是不能识别8进制
![[Pasted image 20220922194717.png]]

###### `ParseInt()`
识别字符串中的整数
* 忽略字符串前面的空格，直到遇到第一个数字字符（或者负号），直到解析到非数字字符，进行*截断*
* *如果第一个字符*就是整数格式（javascript中的十进制、八进制、十六进制），`parseInt()`可以识别进制进行解析
* 可以传入第二个参数作为整数的基数，此时不需要加指定的前缀（0,0x）
###### `parseFloat()`
与`parseInt()`类似，不过注意字符串中第二个小数点肯定是无效的，同时如果识别的是一个整数，函数会自动返回整数。

#### String
16位Unicode字符构成的字符序列。
转义字符：
![[Pasted image 20220922205342.png]]
* `toString()`:转换为字符串。注意规避null的值
* 转型函数`String`:如果值有`toString`函数则调用，如果值是null则返回"null",如果值是undefined,则返回"undefined"。🌟
#### Object
待
### 操作符
#### 一元操作符
一元加和减运算符可以用于转换数据类型。相当于`Number()`或者`valueOf()/toString()`+`Number()`
#### 位操作符
待
#### 布尔操作符
##### 逻辑非(!)
可以应用于任何值。操作符首先会把操作数转化为一个布尔值，然后取反。
![[Pasted image 20220923101639.png]]
##### 逻辑与(&&)
逻辑与不能使用对未定义的值
逻辑与 可以用于任何类型的操作数，但不一定返回布尔值
![[Pasted image 20220923102320.png]]
##### 逻辑或（||）
![[Pasted image 20220923102523.png]]
避免赋null或undefined的操作
![[Pasted image 20220923102623.png]]
#### 乘性运算符
* 乘法
* 除法
* 求模
##### 乘法   *
![[Pasted image 20220923103315.png]]
##### 除法    /
![[Pasted image 20220923103401.png]]
##### 取余    %
![[Pasted image 20220923103446.png]]
#### 加性运算符
##### 加法
![[Pasted image 20220923103647.png]]
##### 减法
![[Pasted image 20220923103757.png]]
#### 关系运算符
返回布尔值
* <
* >
* <=
* >=
* ==  相等和不相等
* ===  全等和不全等
##### < 、>、 <=、 >=
![[Pasted image 20220923104058.png]]
##### ==  相等和不相等
先转换操作数（强制转型），然后比较相等性。
![[Pasted image 20220923104927.png]]
##### 全等和不全等
比较之前不进行类型转换
![[Pasted image 20220923110301.png]]
##### 条件运算符
？：；
##### 赋值运算符
##### 逗号运算符
![[Pasted image 20220923110649.png]]
##### for - in 语句
用来枚举对象的属性
![[Pasted image 20220923111115.png]]
##### label 语句
待
##### break、continue语句

### 函数
* 使用function关键字来声明
* 定义时不需要声明返回值
* 形参不需要指定类型
* 不需要指定形参数目，实际上是以一个数组的形式传入，可以使用`arguments[i]`来访问形参。
* 所有的参数传递都是*值传递*，没有引用传递。
* *没有重载*，后面定义的函数会覆盖掉前面定义的同名函数。
```javascript
function functionName(arg0,arg1,...,argN){
	statements;
}
```
## 变量作用域与内存
* Undefined、Null、Boolean、Number、*String*这些数据类型是保存在栈内存里面（称为基本类型）
* Object对象是保存在堆内存里面，栈里面存储一个地址。(称为引用类型)
* 可以对*引用类型即对象*动态地添加属性，但不能对基本类型的值添加属性。
* 复制变量是复制一份栈内存中的副本，对于基本类型是复制一个相同的副本，*对于引用类型是复制一份内存地址（指针）*
* 函数传递是值传递，对于基本类型就是值传递，对于引用类型传递的是内存地址。
* `person instanceof Object`判断变量是不是*某种类型的对象*，如果判断基本类型，会返回flase 因为基本类型不是对象。
* js没有块级作用域，即for循环里面创建的变量在跳出循环后仍会保留。
* 声明变量时会自动添加到距离最近的可用环境中。*如果变量在未经声明的情况下被初始化，该变量会被自动的添加到**全局环境**中。*
### 执行环境及作用域
执行环境定义了变量或者函数有权访问的其他数据，决定了他们各自的行为。每个执行环境都有一个与之关联的变量对象。
每个函数都有一个执行环境，当调用函数的时候，函数的环境会被推入一个环境栈中，执行之后，栈将环境弹出。
代码在执行的过程，会创建变量对象的一个*作用域链*，保证对执行环境有权访问的所有函数的有序访问。作用域链的前端始终都是*当前执行的代码所在环境的变量对象（例如函数对应的arguments对象）*。作用域链中的下一个变量对象来自包含（外部）环境，而再下一个变量对象来自下一个包含环境，一直延续到全局执行环境。
标识符解析是沿着作用域链一级一级地搜索标识符的过程，如果找不到就报错。
![[Pasted image 20220923212641.png]]
![[Pasted image 20220923212701.png]]
![[Pasted image 20220923212734.png]]

#### 延长作用域链
with语句可以延长作用域链
下面是with语句中的location.url属性在外部被访问。
![[Pasted image 20220923213432.png]]

#### 垃圾收集


## 面向对象程序设计
### 原型链
```javascript
/* 对应名称：
proptype: 原型
__proto__: 原型链（链接点）

从属关系：
prototype -> 函数的一个属性：对象{ } 每个函数都有这样一个属性
__proto__ -> 对象Object的一个属性： 对象{ }

对象的__proto__保存着该对象的构造函数的prototype


Object.prototype.__prop__: null这个就到顶层了
*/
function Test () {
  this.a = 1;
}
console.log(Test.prototype);
Test.prototype.b = 2;

const test = new Test();
console.log(test.__proto__);

console.log(test.__proto__ === Test.prototype);
console.log(Test.prototype.__proto__ === Object.prototype);
console.log(Object.prototype.__proto__);


console.log(test);

// 原型链：以对象的__propto__为节点，逐层向上寻找属性，直到顶层的Object.prototype
// test{
//   a: 1;
//   __proto__: Test.prototype = {
//     b: 2;
//     __proto__: Object.prototype = {
//       c:3
//       没有__proto__
//     }
//   }
// }


// Function Object:函数对象
console.log(Test.__proto__ === Function.prototype);
console.log(Function.__proto__===Function.prototype);// 这不合理，但是 是规定
console.log(Function.prototype)
```
### 创建对象
#### 构造函数模式创建对象
*构造函数首字母大写*
![[Pasted image 20220926112111.png]]

#### `instanceof`检测对象类型
![[Pasted image 20220926112427.png]]
## BOM









# 一些基本的原则
* 定义普通变量的时候不需要显示的初始化为`undefined`因为默认会初始化为`undefined`，而如果是定义一个对象，需要显示的初始化为`null`逻辑上表明这是一个空指针。
* 不要测定浮点数值例如：`if(a+b==0.3)`因为浮点数存在舍入误差。
* JS中对象的属性都是共有的（在对象内部使用`this.propertyName=someValue`定义，或者在外部添加的），对象里面定义的变量(在函数或者块里面`var name=someName`)是私有的，因为在对象外部无法访问这些变量。
# 常用函数
## 时间相关
```
//   time时间后执行函数
setTimeout(func,time)
```