---
title: Vue笔记
date: 2019-03-12 20:11:40
tags:
---

export和export default的区别:

export与export default均可用于导出常量、函数、文件、模块等

export在文件中可以有多个, 引入方式为 import { } from 'module'

export default 在文件中仅有一个	引入方式为 import 变量名 from 'module'

## mixins

混入 (mixins) 是一种分发 Vue 组件中可复用功能的非常灵活的方式。混入对象可以包含任意组件选项。
当组件使用混入对象时，所有混入对象的选项将被混入该组件本身的选项。

常用的window对象属性

window.screen.height	//获取设备屏幕高度

document.body.clientHeight      
document.body.scrollHeight     ->   这三个都会返回文档(整个body)的大小
document.body.offsetHeight 

window.scrollY	//文档当前从原点垂直滚动的像素数

## vue父子组件传参

vue父传子

父组件动态绑定一个属性子组件通过props接收

子传父

子组件通过$emit方法传递一个自定义事件名和数据

父组件通过绑定这个自定义事件名获取子组件传递出来的数据

Number.isInteger()	//判断一个数值是否为整数

Math.trunc	//方法用于去除一个数的小数部分，返回整数部分

