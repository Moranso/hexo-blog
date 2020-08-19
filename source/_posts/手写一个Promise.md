## 手写一个promise

```
function Promis(exector) {
  let _this = this
  this.value = undefined
  this.err = undefined
  this.status = 'pendding'
  this.onFulilledArr = [] //保存成功的回调
  this.onRejectedArr = [] //保存失败的回调

  function resolve(value) {
    if (_this.status === 'pendding') {
      _this.value = value
      _this.onFulilledArr.forEach(fn => fn(value))
      _this.status = 'resolved'
    }
  }

  function reject(err) {
    if (_this.status === 'penddding') {
      _this.err = err
      _this.onRejectedArr.forEach(fn => fn(err))
      _this.status = 'rejected'
    }
  }

  exector(resolve, reject)
}

Promis.prototype.then = function (onFulilled, onRejected) {
  if (this.status === 'pendding') {
    if (typeof onFulilled === 'function') {
      this.onFulilledArr.push(onFulilled)
    }

    if (typeof onRejected === 'function') {
      this.onRejectedArr.push(onRejected)
    }

  }
}


let p = new Promis((resolve, rejecte) => {
  setTimeout(() => {
    resolve(11)
  }, 1000)
})

p.then(res => {
  console.log(res)
})
```

