arr.map(callback): 返回一个新的Array，每个元素为调用func的结果（并没有改变原数组）

arr.filter(callback): 返回一个符合func条件的元素数组（并没有改变原数组）

arr.some(callback): 返回一个boolean，判断数组中是否有元素符合func条件(有一个符合就返回true)（并没有改变原数组）

arr.every(callback): 返回一个boolean，判断数组每个元素是否符合func条件（并没有改变原数组）

arr.forEach(callback): 没有返回值，只是针对每个元素调用func（没有返回值，如果里面有操作方法就会改变原数组）

arr.find(callback): 返回数组中符合条件的第一个元素，否则就返回undefined

arr.findIndex(callback): 返回数组中符合条件的第一个元素的索引值，否则就返回-1

arr.includes(item, finIndex): 判断数组中是否包含有指定的值，包含就返回true，否则就是false

- item 搜索的值
- finIndex 包含的值得索引

### arr.reduce(callback,[initialValue])

**reduce 为数组中的每一个元素依次执行回调函数，不包括数组中被删除或从未被赋值的元素**

- callback （执行数组中每个值的函数，包含四个参数）

    previousValue （上一次调用回调返回的值，或者是提供的初始值（initialValue））

    currentValue （数组中当前被处理的元素）

    index （当前元素在数组中的索引）

    array （调用 reduce 的数组）

- initialValue （作为第一次调用 callback 的第一个参数。）

```

let reduceArr = [1, 2, 3, 4, 5]

let reducer = (x, y) => x + y

let sum = reduceArr.reduce(reducer, 1)  //16

```

