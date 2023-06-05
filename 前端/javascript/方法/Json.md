- JSON.stringify 将对象转换为 JSON。
- JSON.parse 将 JSON 转换回对象。
# JSON.stringify 
`let json = JSON.stringify(value[, replacer, space])`：Json序列化
- value:要编码的值。
- replacer:要编码的**属性数组**或**映射函数 function(key, value)=>{return value}**。注意，如果是映射函数，迭代器第一项是使用特殊的“包装对象”制作的：{"": meetup}。换句话说，第一个 (key, value) 对的键是空的。
- 自定义toJSON，对象也可以提供 toJSON 方法来进行 JSON 转换。如果可用，JSON.stringify 会自动调用它。
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
# JSON.parse
`let value = JSON.parse(str, [reviver]);`
- str 要解析的 JSON 字符串。
- reviver 可选的函数 function(key,value)，该函数将为每个 (key, value) 对调用，并可以对值进行转换。(这个一般都要用，因为**值默认都是string(双引号)或者Number(不加加引号的数字)**，要把它转化为正确的类型)。