# Number
## toString(base*)
方法 num.toString(base) 返回在给定 base 进制数字系统中 num 的字符串表示形式。
## 舍入 
`toFixed(n) `
将数字舍入到小数点后 n 位，**并以字符串形式**返回结果。
`Math.floor`
向下舍入：3.1 变成 3，-1.1 变成 -2。
`Math.ceil`
向上舍入：3.1 变成 4，-1.1 变成 -1。
`Math.round`
向最近的整数舍入：3.1 变成 3，3.6 变成 4，中间值 3.5 变成 4。
`Math.trunc`（IE 浏览器不支持这个方法）
移除小数点后的所有内容而没有舍入：3.1 变成 3，-1.1 变成 -1。 ^lcbmi2
## 测试
`isNaN(value)` 将其参数转换为数字，然后测试它是否为 NaN
`isFinite(value)` 将其参数转换为数字，如果是常规数字而不是 NaN/Infinity/-Infinity，则返回 true
>与 Object.is 进行比较
有一个特殊的内建方法 Object.is，它类似于 === 一样对值进行比较，但它对于两种边缘情况更可靠：
它适用于 NaN：Object.is(NaN, NaN) === true，这是件好事。
值 0 和 -0 是不同的：Object.is(0, -0) === false，从技术上讲这是对的，因为在内部，数字的符号位可能会不同，即使其他所有位均为零。
在所有其他情况下，Object.is(a, b) 与 a === b 相同。

## 提取数字parseInt(str, radix) 和 parseFloat(str)
使用加号 + 或 Number() 的数字转换是严格的。如果一个值不完全是一个数字，就会失败：
>alert( +"100px" ); // NaN

唯一的例外是字符串开头或结尾的空格，因为它们会被忽略。
它们可以从字符串中“读取”数字，直到无法读取为止。如果发生 error，则返回收集到的数字。函数 parseInt 返回一个整数，而 parseFloat 返回一个浮点数
## 数学函数
`Math.random()`
返回一个从 0 到 1 的随机数（不包括 1）。
`Math.max(a, b, c...)` 和 `Math.min(a, b, c...)`
从任意数量的参数中返回最大值和最小值。
`Math.pow(n, power)`
返回 n 的给定（power）次幂。