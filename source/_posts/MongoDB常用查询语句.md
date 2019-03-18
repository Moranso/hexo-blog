---
title: MongoDB常用查询语句
date: 2019-03-12 20:38:44
tags:
---

#### mongodb常用命令:

help					//查看帮助,如何使用命令
show dbs				//显示有哪些数据库,如果不存在会自动创建

use 数据库名				//使用哪个数据库,如果数据库不存在就会自动创建
show collections			//显示当前数据库中有哪些集合

##### //添加

db.集合名(表名).insert({'属性名':'值'})		//插入数据,如果集合名称不存在会自动创建集合名称

##### //删除

db.集合名.remove({})					//删除集合下所有数据
db.集合名.remove({'属性名':'值'})			//删除集合下指定条件的数据
db.users.drop() 或 db.runCommand({"drop":"集合名"})	//删除集合
db.runCommand({"dropDatabase":1})			//删除数据库

##### //修改

db.集合名(表名).update({查找条件},{修改数据})	//条件和数据都是json格式

##### //查询

db.集合名(表名).find()				//显示当前集合(表)中有哪些数据(全表查询)
db.集合名(表名).find().pretty()			//查询的结果,以漂亮格式显示出来
db.集合名(表名).find({'条件' : '值'})dc		//按条件查询,条件应该是json格式

------

##### mongodb高级命令

大于:		$gt
小于:		$lt
大于等于:	$gte
小于等于:	$lte
不等于:		$

1.按条件查询

db.集合名.find({'key':{$gt:'value'}})

db.集合名.find({'key':{$gt:value,$lt:value}})			//范围之间

db.集合名.find({'key':{$ne:'value'}})				//不等于

db.集合名.find({'key':{$mod:[5,0]}})     			//五的倍数余数为0

db.集合名.find({'key':{$in:['value1','value2']}})		//key为value1 或key为value2

db.集合名.find({'key':{$nin:['value1','value2']}})		//key不是value1 value2中的任意一个

db.集合名.find({'key':{$size:4}})				//键的值是数组的才能使用

db.集合名.find({'key':{$exists:true}})				//包含key字段的

db.集合名.find({$or:[{key:值1,key:值2}]})			//要么值为1的,要么值为2的

db.集合名.find({}).sort({'key':-1})				//1:升序,-1:降序

db.集合名.find({}).sort({'key1':-1,'key2':1})			按key1值降序,按key2值升序



##### ensureIndex() 方法来创建索引,语法如下

db.集合名.ensureIndex({字段名称:1})

1为指定按升序创建索引,如果想按降序创建索引指定位-1

------

做项目要使用的命令

db.集合名.find().limit(5)		//限制多少条数据
db.集合名.find().skip(5)		//跳过多少条数据

db.集合名.find().skip(5).limit(5)	//用来做分页,跳过5条数据再取5条数据

db.集合名.find().count()		//返回总的条数

------



#### mongoose

1.安装:npm install mongoose --save	(在项目目录中安装)

------

2.引入mongoose: var mongoose = require('mongoose')

3.连接数据库:

```
mongoose.connect('mongodb://主机名:端口号/数据库名',(err)=>{	

​	if (err) {
​		console.log('数据库链接失败');
​	}

});
```

4.定义数据库中集合的骨架 : (创建表)

```
var newsSchema = new mongoose.Schema({

字段:字段类型,
字段:字段类型,
...
})
```



5.得到骨架的模型:

```
var newsModel = mongoose.mode('集合名',骨架,'别名');
```



##### 添加数据

6.得到模型的实例:(路由里面实例化)

```
var newsInstance = new newsModel({		
	字段名称 = 值;
});

newsInstance.save(callback(err));
```



##### 修改数据

```
newsModel.findById(id,function(err,data){

	data.属性名 = 属性值;

	data.save(clalback);

});
```



##### 删除数据

```
newsModel.findById(id,function(err,data){

	data.remove(clalback);

});
```



##### 查询数据（模型.find（））

//按id查询

```
newsModel.findById(id,function(err,data){

​	res.send(data);		//返回数据

});
```

​	

//查询多条数据,并且返回的结果是一个数组

```
newsModel.find({'列的名称':'列的值'},function(err,data){

​	res.send(data);		//返回数据

});
```



//查找符合条件的数据,只返回结果中的一条数据

```
newsModel.findOne({'列的名称':'列的值'},function(err,data){

res.send(data);		//返回数据

});
```



##### 搭建nodejs的服务器环境express

```
安装express脚手架

npm i -g express-generator

```



```
a. 创建项目	
	express -e 项目名字

b. 进入项目文件夹安装依赖
	npm i

c. app.js 添加端口号

```

```
d. 安装mongoose(在当前项目的目录中)	
	npm install mongoose --save

```

```
route文件夹下新建一个路由	
	news.js	

app.js中引入路由并使用路由

```