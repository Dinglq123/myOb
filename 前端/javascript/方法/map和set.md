# map
## 方法
- new Map() —— 创建 map。
- **map.set(key, value)** —— 根据键存储值。
- **map.get(key)** —— 根据键来返回值，如果 map 中不存在对应的 key，则返回 undefined。
- map.has(key) —— 如果 key 存在则返回 true，否则返回 false。
- map.delete(key) —— 删除指定键的值。
- map.clear() —— 清空 map。
- map.size —— 返回当前元素个数。
## 迭代
**迭代的顺序与插入值的顺序相同。与普通的 Object 不同，Map 保留了此顺序。**
- map.keys() —— 遍历并返回一个包含所有键的可迭代对象，
- map.values() —— 遍历并返回一个包含所有值的可迭代对象，
- map.entries() —— 遍历并返回一个包含所有实体 [key, value] 的可迭代对象，for..of 在默认情况下使用的就是这个。
- recipeMap.forEach( (**value, key, map**) => {
## 对象和map的转化
对象---->map
`let map = new Map(Object.entries(obj));`
map---->对象
`let obj = Object.fromEntries(map.entries()); `
# Set
Set 是一个特殊的类型集合 —— “值的集合”（没有键），它的每一个值只能出现一次。
## 方法
- new Set(iterable) —— 创建一个 set，如果提供了一个 iterable 对象（通常是数组），将会从数组里面复制值到 set 中。
- **set.add(value)** —— 添加一个值，返回 set 本身
- set.delete(value) —— 删除值，如果 value 在这个方法调用的时候存在则返回 true ，否则返回 false。
- set.has(value) —— 如果 value 在 set 中，返回 true，否则返回 false。
- set.clear() —— 清空 set。
- set.size —— 返回元素个数。
## Set 迭代（iteration）
我们可以使用 for..of 或 forEach 来遍历 Set：
- for (let value of set) alert(value);
- set.forEach((value, *valueAgain*, set) => {