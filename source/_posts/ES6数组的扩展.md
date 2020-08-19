---
title: ES6数组的扩展
date: 2019-03-20 20:12:11
tags:
---

#### 扩展运算符

```
console.log(...[1, 2, 3])	//1, 2, 3

console.log(1, ...[2, 3, 4],  5)	//1, 2, 3, 4, 5
```

#### 深拷贝数组

```
const arr = [1, 2, 3]
const copArr = [...arr]
```

```javascript
Math.max(...[14, 3, 77])	//求数组最大元素
```

#### 合并数组

```
const arr1 = ['a', 'b']
const arr2 = ['c', 'd']
const arr3 = [...[arr1], ...[arr2]]		//浅拷贝
```

#### 数组的解构赋值

```
let a = 1
let b = 2

这种写法属于“模式匹配”，只要等号两边的模式相同，左边的变量就会被赋予对应的值。
let [a, b] = [1, 2]
```

###### 如果解构不成功,变量的值就等于undefined

#### 对象的解构赋值

```
let {bar, foo} = {foo: 'aaa', bar: 'bbb'}
console.log(foo)	//aaa
console.log(bar)	//bbb
```

#### 数组解构赋值和对象解构赋值的区别

###### 数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值

#### 函数参数的解构赋值

```
function add([x, y]) {
	return x + y
}

add([1, 2])	// 3
```

#### js this指向

普通函数中的this指向window对象

对象方法中的this指向当前这个对象

构造函数中的this指向当前实例化的这个对象