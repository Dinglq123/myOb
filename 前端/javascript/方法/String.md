# 字符串
单引号，双引号和反引号的区别：
单引号=双引号，反引号**可以换行**，可以**包含模板`${}`**。
## length
返回字符串长度
## 大小写
toLowerCase() 和 toUpperCase() 方法可以改变大小写：
```js
alert( 'Interface'.toUpperCase() ); // INTERFACE
alert( 'Interface'.toLowerCase() ); // interface
// 或者我们想要使一个字符变成小写：
alert( 'Interface'[0].toLowerCase() ); // 'i'
```
## 查找子字符串
str.indexOf
第一个方法是 `str.indexOf(substr, pos)`。
它从给定位置 pos 开始，在 str 中查找 substr，如果没有找到，**则返回 -1**，否则返回匹配成功的位置。
还有一个类似的方法 `str.lastIndexOf(substr, position)`，它从字符串的末尾开始搜索到开头。它会以相反的顺序列出这些事件。
`includes(substr, pos)`，`startsWith`，`endsWith`根据 str 中是否包含 substr 来返回 true/false。
## 获取子字符串

| 方法                  | 选择方式……                            | 负值参数          |
| --------------------- | ------------------------------------- | ----------------- |
| slice(start, end)     | 从 start 到 end（不含 end）           | 允许              |
|                       |                                       |                   |
| substring(start, end) | 从 start 到 end（不含 end）           | 负值被视为 0      |
| substr(start, length) | 从 start 开始获取长为 length 的字符串 | 允许 start 为负数 |

## 调整字符串
str.trim() —— 删除字符串前后的空格 (“trims”)。
str.repeat(n) —— 重复字符串 n 次。