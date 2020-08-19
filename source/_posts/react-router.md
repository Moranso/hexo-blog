---
title: react+router
date: 2019-04-01 20:01:22
tags:
---

创建router.js文件

```
import React from 'react';
import {HashRouter, Route, Switch} from 'react-router-dom';
import Home from '../home';
import Detail from '../detail';

const BasicRoute = () => (
    <HashRouter>
        <Switch>
            <Route exact path="/" component={Home}/>
            <Route exact path="/detail" component={Detail}/>
        </Switch>
    </HashRouter>
);

export default BasicRoute;
```

在index.js(入口文件)组件里渲染路由组件

```
import React from 'react';
import ReactDOM from 'react-dom';
import Router from './router/router';

ReactDOM.render(
  <Router/>,
  document.getElementById('root')
);
```

### 路由跳转

#### 通过a标签跳转

```
<a href='#/'>回到home</a>
```

#### 通过函数跳转

修改router.js文件中的两处代码

```
...
import {HashRouter, Route, Switch, hashHistory} from 'react-router-dom';
...
<HashRouter history={hashHistory}>
```

```
<button onClick={() => this.props.history.push('detail')}>通过函数跳转</button>
```

#### URL传参

修改router.js中的代码

```
...
<Route exact path="/detail/:id" component={Detail}/>
...
```

接收URL传过来的参数

```
this.props.match.params
```

#### 隐式传参

```
this.props.history.push({
	pathname: '/detail',
    state: {
    	id: 3
    }
})
```

接收参数

```
this.props.history.location.state

```

#### 其他函数

##### replace

有些场景下，重复使用push或a标签跳转会产生死循环，为了避免这种情况出现，react-router-dom提供了replace。在可能会出现死循环的地方使用replace来跳转：

```
this.props.history.replace('/detail')

```

goBack

场景中需要返回上级页面的时候使用：

```
this.props.history.goBack();

```

[参考文章]: https://www.jianshu.com/p/8954e9fb0c7e

