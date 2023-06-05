# map
## 方法
- new Map() —— 创建 map。
- map.set(key, value) —— 根据键存储值。
- map.get(key) —— 根据键来返回值，如果 map 中不存在对应的 key，则返回 undefined。
- map.has(key) —— 如果 key 存在则返回 true，否则返回 false。
- map.delete(key) —— 删除指定键的值。
- map.clear() —— 清空 map。
- map.size —— 返回当前元素个数。
## 迭代
**迭代的顺序与插入值的顺序相同。与普通的 Object 不同，Map 保留了此顺序。**
- map.keys() —— 遍历并返回一个包含所有键的可迭代对象，
- map.values() —— 遍历并返回一个包含所有值的可迭代对象，
- map.entries() —— 遍历并返回一个包含所有实体 [key, value] 的可迭代对象，for..of 在默认情况下使用的就是这个。
## 对象和map的转化
对象---->map
`let map = new Map(Object.entries(obj));`
map---->对象
`let obj = Object.fromEntries(map.entries()); `
