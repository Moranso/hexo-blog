router.resolve()

新窗口打开的属性了，这个时候就需要使用this.$router.resolve,如下：

```
let routeUrl = this.$router.resolve({
	path: "/share",
	query: {id:96}
});
window.open(routeUrl .href, '_blank');
```

