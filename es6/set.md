# 概述
Set 本身是一个构造函数，用来生成 Set 数据结构

# 特点
Set 结构不会添加重复的值

# 属性
`Set.prototype.constructor`: 构造函数
`Set.prototype.size`: 返回Set实例的成员总数

# 操作方法
`add(value)`：添加值
`delete(value)`：删除值，返回boolean标示是否成功
`has(value)`：返回boolean值标示是否含有某值
`clear()`：清除所有成员

`Array.from(setArr1)`：set实例化之后是一个对象类型，用此方法转为数组

# 遍历操作
`keys()`：返回键名的遍历器
`values()`：返回键值的遍历器
`entries()`：返回键值对的遍历器
`forEach()`：使用回调函数遍历每个成员
例：
```javascript
let setArr1 = new Set();
setArr1.forEach((item) => {
    ///
});
```
