- JSON.stringify 将对象转换为 JSON。
- JSON.parse 将 JSON 转换回对象。
# Json字符串和变量的相互转化
`let json = JSON.stringify(value[, replacer, space])`：Json序列化
- value:要编码的值。
- replacer:要编码的**属性数组**或**映射函数 function(key, value)**。注意，如果是映射函数，迭代器第一项是使用特殊的“包装对象”制作的：{"": meetup}。换句话说，第一个 (key, value) 对的键是空的。
## 注意点：
- 字符串使用**双引号**。JSON 中没有单引号或反引号。所以 'John' 被转换为 "John"。
- 对象属性名称也是双引号的。这是强制性的。所以 age:30 被转换成 "age":30。
- **函数属性（方法）**，**Symbol**类型的值和键，存储**undefined的属性**都会被忽略。
## 可以使用的类型：
- Objects { ... }
- Arrays [ ... ]
- Primitives：
- strings，
- numbers，
- boolean values true/false，
- null。
