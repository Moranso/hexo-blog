```
      class Observer {
​        constructor(*fns*) {
​          *this*.fns = fns || []
​        }

​        // 订阅
​        subscribe(*fn*) {
​          *this*.fns.push(fn)
​        }

​        // 取消订阅
​        unsubscribe(*fn*) {
​          *this*.fns = *this*.fns.filter(*el* => el !== fn)
​        }

​        // 发布
​        release(*val*) {
​          *this*.fns.forEach(*fn* => fn(val))
​        }
​      }
​      let fn1 = *val* => {
​        *console*.log("我是发布的第一个" + val)
​      }
​      let o = **new** *Observer*()
​      o.subscribe(fn1)
​      o.release("对象")
​      o.unsubscribe(fn1)
​      o.release("对象")
```

