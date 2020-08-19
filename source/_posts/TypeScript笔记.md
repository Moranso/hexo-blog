---
title: TypeScript笔记
date: 2019-03-12 20:40:01
tags:
---

声明一个void类型的变量只能给它赋值undefined 和 null

当一个函数没有返回值时，你通常会见到其返回值类型是 void

null和undefined是所有类型的子类型。 就是说你可以把 null和undefined赋值给number类型的变量。

#### 类型断言:

let someValue: any = "this is a string";

let strLength: number = (someValue as string).length;