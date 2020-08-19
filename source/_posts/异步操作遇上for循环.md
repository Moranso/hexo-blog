```
<script>
  let arr = [1, 2, 3]
  
  function waite(num) {
    return new Promise((resolve, reject) => {
      setInterval(() => {
        resolve(num)
      }, 1000)
    })
  }

  let newArr = []

  async function asy() {
    for (let item of arr) {
      let res = await waite(item)
      newArr.push(res)
    }
    return newArr
  }

  asy().then(res => {
    console.log(res)  // [1, 2, 3]
  }).catch(err => {
    console.log(err)
  })
</script>
```

