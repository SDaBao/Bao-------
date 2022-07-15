# 手写深拷贝

## 简单的 deepCopy 代码

代码流程：

1. 先判断拷贝对象为数组或对象
2. 遍历拷贝对象内各属性与其值
3. 进行复制操作：判断拷贝的值是否需要更深层次拷贝，使用递归的思想进行处理

```javascript
let obj = {a: 1, b: {c: 2}, d: [1, 2, 3]}
//let obj = [1, {a: 2}, [3, 4]]

function deepCopy(objOrArr) {
  let ret = Array.isArray(objOrArr) ? [] : {}
  for(let key in objOrArr) {
    // 判断值是否为 null 是因为在 JS 中，typrof null === object 的值为 true
    if(typeof objOrArr[key] !== 'object' || objOrArr[key] === null) {
      ret[key] = objOrArr[key]
    } else {
      ret[key] = deepCopy(objOrArr[key])
    }
  }
  return ret
}

let obj2 = deepCopy(obj)
```

## 变式1：深拷贝里有循环引用怎么办

```javascript
let obj = {a: 1, b: {c: 2}, d: [1, 2, 3]}
obj.e = obj

function deepCopy(objOrArr) {
//   使用 WeakMap 数据结构，存放引用类型
  let map = new WeakMap()
  let ret = Array.isArray(objOrArr) ? [] : {}
  map.set(objOrArr, ret)

  for(let key in objOrArr) {
    if(map.has(objOrArr[key])) {
      ret[key] = map.get(objOrArr[key])
    } else if(typeof objOrArr[key] !== 'object' || objOrArr[key] === null) {
      ret[key] = objOrArr[key]
    } else {
      ret[key] = deepCopy(objOrArr[key])
      map.set(objOrArr[key], ret[key])
    }      
  }
  return ret
}

let obj2 = deepCopy(obj)
```
