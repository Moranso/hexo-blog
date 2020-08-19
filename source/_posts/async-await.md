---
title: async/await
date: 2019-03-20 20:13:14
tags:
---

#### async

`async`函数返回一个 Promise 对象，可以使用`then`方法添加回调函数。当async函数执行的时候，一旦遇到`await`就会停止执行，等到异步操作完成，再接着执行函数体内后面的语句

```
aysnc function asy() {
	return 1
}
asy()	//返回一个Promise对象
```

`async`函数内部`return`语句返回的值，会成为`then`方法回调函数的参数。

```
asy().then(res => {
	console.log(res)	//1
)
```

`async`函数内部抛出错误，会导致返回的 Promise 对象变为`reject`状态。抛出的错误对象会被`catch`方法回调函数接收到。

```
async function f() {
  throw new Error('出错了');
}

f().then(
  v => console.log(v),
  e => console.log(e)
)	//出错了
```

#### Promise对象的状态变化

`**async`函数返回的 Promise 对象，必须等到内部所有`await`命令后面的 Promise 对象执行完，才会发生状态改变**，除       非遇到`return`语句或者抛出错误。也就是说，只有`async`函数内部的异步操作执行完，才会执行async 的`then`方法指定的回调函数。

#### `await`

正常情况下，`await`命令后面是一个 **Promise** 对象，返回该对象的结果。如果不是 Promise 对象，就直接返回对应的值。

任何一个`await`语句后面的 Promise 对象变为`reject`状态，那么整个`async`函数都会中断执行。

```
function timeout(num) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
        	resolve(num * 2)
        }, 2000)
    })
}

async function print() {
    const result = await timeout(20)
    return result
}

print().then(res => {
    console.log(res)	//40
})
```

有时，我们希望即使前一个异步操作失败，也不要中断后面的异步操作。这时可以将第一个`await`放在`try...catch`结构里面

```
async function f() {
  try {
    await Promise.reject('出错了');
  } catch(e) {
  	console.log(e)
  }
  return await Promise.resolve('hello world');
}

f().then(res => {
    console.log(res)	//hello world
})
```

