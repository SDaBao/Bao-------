# 数组去重
## 简单的数组去重
使用 Set 数据结构
```javascript
let obj = {a: 1}
const arr = [3, 3, 'a', 'a']

function removeDuplicate(arr) {
  return  [...new Set(arr)]
}

console.log( removeDuplicate(arr) )
```


## 不用set 如何去重
使用 Array 函数 filter()

```javascript
let obj = {a: 1}
const arr = [3, 3, obj, obj, 'a', 'a']

function removeDuplicate(arr) {
  return arr.filter((value, index) => arr.indexOf(value) === index)
}

console.log( removeDuplicate(arr) )
```

## 在原数组上操作

```javascript
let obj = {a: 1}
const arr = [3, 3, obj, obj, 'a', 'a']

function removeDuplicate(arr) {
  let set = new Set()
  for(let i=0; i<arr.length; i++) {
    if(!set.has(arr[i])) {
      set.add(arr[i])
    } else {
      arr.splice(i, 1)
      i--
    }
  }
}

removeDuplicate(arr)
console.log(arr)
```

## 变式1：去重：相同对象

```javascript
const arr = [3, 3, {a: 1}, {a: 1}, [3,4,5], [3,4,5], 'a', 'a']

function removeDuplicate(arr) {
  let set = new Set()
  return arr.filter(v => {
    if(typeof v === 'object' && v!== null) {
      v = JSON.stringify(v)
    } 
    if(set.has(v)) return false
    set.add(v)
    return true
  })
}

console.log( removeDuplicate(arr) )
```

## 变式2：如果数组里是多个对象，如何按对象属性字段去重?

```javascript
let arr = [{id: 1, value: 'react'}, {id: 2, value: 'react'},  {id: 3, value: 'vue'}]

function removeDuplicate(arr) {
  let set = new Set()
  return arr.filter(v => !set.has(v.value)&&set.add(v.value))
}

console.log( removeDuplicate(arr) )
```

