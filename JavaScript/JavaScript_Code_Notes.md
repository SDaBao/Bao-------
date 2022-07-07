//数组去重
//let obj = {a: 1}
// const arr = [3, 3, 'a', 'a']
// function removeDuplicate(arr) {
//   return  [...new Set(arr)]
// }
// console.log( removeDuplicate(arr) )


//不用set 如何去重
// let obj = {a: 1}
// const arr = [3, 3, obj, obj, 'a', 'a']
// function removeDuplicate(arr) {
//   return arr.filter((value, index) => arr.indexOf(value) === index)
// }
// console.log( removeDuplicate(arr) )

//在原数组上操作
// let obj = {a: 1}
// const arr = [3, 3, obj, obj, 'a', 'a']
// function removeDuplicate(arr) {
//   let set = new Set()
//   for(let i=0; i<arr.length; i++) {
//     if(!set.has(arr[i])) {
//       set.add(arr[i])
//     } else {
//       arr.splice(i, 1)
//       i--
//     }
//   }
// }
// removeDuplicate(arr)
// console.log(arr)

//去重：相同对象
// const arr = [3, 3, {a: 1}, {a: 1}, [3,4,5], [3,4,5], 'a', 'a']
// function removeDuplicate(arr) {
//   let set = new Set()
//   return arr.filter(v => {
//     if(typeof v === 'object' && v!== null) {
//       v = JSON.stringify(v)
//     } 
//     if(set.has(v)) return false
//     set.add(v)
//     return true
//   })
// }

// console.log( removeDuplicate(arr) )

//如果数组里是多个对象，如何按对象属性字段去重?
// let arr = [{id: 1, value: 'react'}, {id: 2, value: 'react'},  {id: 3, value: 'vue'}]
// function removeDuplicate(arr) {
//   let set = new Set()
//   return arr.filter(v => !set.has(v.value)&&set.add(v.value))
// }
// console.log( removeDuplicate(arr) )

//手写深拷贝
// let obj = {a: 1, b: {c: 2}, d: [1, 2, 3]}
// //let obj = [1, {a: 2}, [3, 4]]
// function deepCopy(objOrArr) {
//   let ret = Array.isArray(objOrArr) ? [] : {}
//   for(let key in objOrArr) {
//     if(typeof objOrArr[key] !== 'object' || objOrArr[key] === null) {
//       ret[key] = objOrArr[key]
//     } else {
//       ret[key] = deepCopy(objOrArr[key])
//     }
//   }
//   return ret
// }
// let obj2 = deepCopy(obj)

//如果深拷贝里有循环引用怎么办
let obj = {a: 1, b: {c: 2}, d: [1, 2, 3]}
obj.e = obj

function deepCopy(objOrArr) {
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