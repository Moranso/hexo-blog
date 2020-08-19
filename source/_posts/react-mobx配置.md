---
title: react+mobx配置
date: 2019-04-01 20:00:18
tags:
---

npm run eject弹出webpack配置,报错解决办法:

```
git add .
git commit -am "Save before ejecting"
npm run eject
```

安装支持装饰器所需依赖

```
npm i --save-dev babel-plugin-transform-decorators-legacy
```

安装 @babel/plugin-propposal-decorators

```
npm i @babel/plugin-proposal-decorators --save-dev
```

安装Mobx和mobx-react

```
npm i mobx --save
npm i mobx-react --save
```

配置package.json文件

```
"babel": {
	"plugins": [
        [
          "@babel/plugin-proposal-decorators",
        	{
            	"legacy": true
        	}  
        ],
        [
            "@babel/plugin-proposal-class-properties",
        	{
            	"loose" true
        	}
        ]
	],
	"presets": [
        "react-app"
	]
}
```

