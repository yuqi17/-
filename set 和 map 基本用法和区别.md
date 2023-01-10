
```js
let str = 'aaabbbcccdddeee'

const arr = str.split('')// 字符串转数组

const set = new Set(arr);// 数组转set
set.add(88888)
set.delete('a')

console.log(set.has(88888), set.has('a'), '<<<<<<<<=====')


for(let s of set){
    console.info(s,'$$$')
}

console.log(set, '%%% 后面俩是等价的', [...set], Array.from(set))// set 转 数组, set 本身不是数组,不能按数组的方式操作


console.log(set.keys(), set.values(), set.entries(),'<<< 前面三个都是迭代器, 都不是数组')
console.log(Array.isArray(Object.keys({s:1})))// Object.keys, Object.values(), Object.entries() 返回的是数组


for(let e of set.entries()){ // 迭代器只能通过迭代的方式取值, 也可以转成数组
    console.log(e, '<====')// 返回的是数组类似这种[1, 1]
}


let map = new Map();
map[1] = 111
console.log(map[1])// 这些用法跟object 一样

map.set(1, '222')

console.log('-----------------')
console.log(map.has(1))
map.delete(1)// 类似 object 的delete 语法 var o = {key : 111};   delete o[key];
console.log(map.has(1))


console.log(map.get(1), '<<<--map')// map 和 object 很类似, 不过map 有size object 没

console.log(map.keys(), map.values(), map.entries(), '<<<===map') // 以上全部都是map 的迭代器, 只能迭代取值, 也可以转成数组

// https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Map

// https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set

```
