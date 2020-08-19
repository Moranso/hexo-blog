---
title: Promise承诺对象
date: 2019-03-20 20:15:02
tags:
---

### 事件流

事件流分为事件冒泡和事件捕获

页面接受事件的顺序,IE的事件流是事件冒泡流(event bubbling),网景的事件流是事件捕获流(event capturing)

- 事件冒泡流

  事件开始时由最具体的元素接收,然后逐级向上传播到较为不具体的节点

- 事件捕获流

  不太具体的DOM节点应该更早接收到事件,而最具体的节点应该最后接收到事件

#### 阻止事件冒泡

event.preventDefault() || return false(也可用来阻止表单默认事件)

### Promise承诺对象

**三种状态**: pending(进行中)	fulfilled(已成功)	rejected(已失败)

对象的状态不受外界影响,由异步操作的结果决定是哪种状态

#### 对象状态改变的两种可能

pending ---> fulfilled

pending ---> rejected

只要这两种情况发生,状态就凝固了,不会再变 这时称为resolved(已定型)

#### Promise的缺点

- 一旦新建会马上执行,无法中途取消
- 如果不设置回调函数,promise内部抛出的错误不会反应到外部
- 当处于pending状态时,无法得知目前进展到哪一个阶段(刚刚开始还是即将完成)

#### 基本用法

```javascript
Promise对象是一个构造函数,用来生成Promise实例
Promise构造函数接收一个函数作为参数,该函数的两个参数分别是resolve和reject,它们也是两个函数
//生成Promise实例
const promise = new Promise((resolve, reject) => {
    //...some code
    if (异步操作成功) {
    	resolve(value)
    } else {
    	reject(error)
    }
})
```

#### resolve函数的作用

在异步操作成功时调用,并将成功的结果作为参数传递出去

#### reject函数的作用

在异步操作失败时调用,并将异步操作失败的结果作为参数传递出去

#### Promise的then方法

then方法可以接受两个回调函数作为参数

第一个回调函数的参数是异步操作成功的结果(promise状态变为resolved时调用)

第二个回调函数的参数是异步操作失败的结果(promise状态变为rejected时调用),第二个回调函数是可选的

```javascript
promise.then(success => {
	//success异步操作成功的结果
}, error => {
	//error异步操作失败的结果
})
```

一般来说,调用resolve或reject以后,Promise的使命就完成了,后继操作应该放到then方法里面,而不应该直接写在resolve或reject的后面,所以最好在它们面前加上return语句

```javascript
new Promise((resolve, reject) => {
  return resolve(1);
  // 后面的语句不会执行
  console.log(2);
}).then(success => {
  console.log(success)
})
```

```javascript
new Promise((resolve, reject) => {
  return resolve(1);
  // 后面的语句不会执行
  console.log(2);
})
```

#### Promise的then方法定义在Promise原型上 (Promise.prototype.then())

##### 作用: 它的作用是为Promise实例添加状态改变时的回调函数

###### then方法返回一个新的Promise实例,因此可以采用链式写法

比如下一个异步操作依赖上一个异步操作的结果作为依赖

采用链式的then,可以指定一组按照次序调用的回调函数,前一个回调函数返回的可能是一个Promise对象(有异步操作),这时后一个then的回调函数就会等待Promise对象的状态发生变化时调用

#### Promise.prototype.catch()

catch是**promise**(异步操作)失败时调用的方法,是then方法第二个参数的别名,如果then方法指定成功的回调函数发生错误,也会被catch方法捕获

###### 一般来说用catch方法代替在then方法里面定义的reject状态的回调函数

```
let promise = new Promise((resolve, reject) => {
    return reject('error')
})
promise.catch(err => {
	console.log(err)	//打印出来 error
})
```

#### Promise.all

##### **Promise.all可以将多个Promise实例包装成一个新的Promise实例。同时，成功和失败的返回值是不同的，成功的时候返回的是一个结果数组，而只要有一个失败的时候则返回最先被reject失败状态的值**

```javascript
let p1 = new Promise((resolve, reject) => {
  resolve('成功了')
})

let p2 = new Promise((resolve, reject) => {
  resolve('success')
})

let p3 = Promse.reject('失败')

Promise.all([p1, p2]).then((result) => {
  console.log(result)               //['成功了', 'success']
}).catch((error) => {
  console.log(error)
})

Promise.all([p1,p3,p2]).then((result) => {
  console.log(result)
}).catch((error) => {
  console.log(error)      // 失败了，打出 '失败'
})
```

#### Promise.prototype.finally()

##### `finally`方法用于指定不管 Promise 对象最后状态如何，都会执行的操作

