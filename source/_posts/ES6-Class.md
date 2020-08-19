---
title: ES6 Class
date: 2019-04-01 20:04:53
tags:
---

### ES5创建类

```
// Person即是类也是构造函数(构造器)
function Person(name, sex) {
	this.name = name
	this.sex = sex
}

// 原型方法 (类方法)
Person.prototype.sayHello = function() {
    console.log('你好,我叫' + this.name)
}

// 实例化对象
let p = new Person('su', '男')
```



### ES6创建类

```
class Person {
	// constructor 对应ES5的构造函数(构造器)
    constructor(name, sex) {
        this.name = name
        this.sex = sex
    }
    sayHello() {
        console.log('你好,我叫' + this.name)
    }
}

// 类的数据类型就是函数,指向构造函数 (prototype对象的constructor属性指向类本身)
Person === Person.prototype.constructor  // true
```

#### 注意:

- constructor**方法是类的默认方法,通过new命令生成对象实例时,自动调用该方法,如果没有定义会自动生成
- `constructor`方法默认返回实例化的对象（即`this`）



#### 取值函数(getter) 和 存值函数(setter)

对某个值设置存值函数和取值函数

```
class MyClass {
  constructor() {
    // ...
  }
  get prop() {
    return 'getter';
  }
  set prop(value) {
    console.log('setter: '+value);
  }
}

let inst = new MyClass();

inst.prop = 123;
// setter: 123

inst.prop
// 'getter'
```

#### 注意:

- 普通函数中的this指向window对象
- 对象方法中的this指向当前这个对象
- 构造函数中的this指向当前实例化的这个对象

```
class Logger {
  printName(name = 'there') {
    this.print(`Hello ${name}`);
  }

  print(text) {
    console.log(text);
  }
}

const logger = new Logger();
const { printName } = logger;
printName();
```

`printName`方法中的`this`，默认指向`Logger`类的实例。但是，如果将这个方法提取出来单独使用，`this`会指向该方法运行时所在的环境（由于 class 内部是严格模式，所以 this 实际指向的是`undefined`）

一个比较简单的解决方法是，在构造方法中绑定`this`，这样就不会找不到`print`方法了。

```
class Logger {
  constructor() {
    this.printName = this.printName.bind(this);
  }

  // ...
}
```

#### ES6继承

##### super

- super 表示父类的构造函数(constructor),用来新建父类的this对象
- 子类必须且只能在constructor方法中调用,super方法拿来构造子类自己的this对象,得到与父类同样的属性和方法
- 如果不调用super方法,子类得不到this对象
- super关键字,既可以当做函数使用,也可以当做对象使用
- 作为函数调用时,代表父类的构造函数,返回的是子类的实例,this指向子类的实例
- super作为对象时在普通方法中,指向父类的原型对象,在静态方法中指向父类

super(父属性1,  属性2)	//继承父类的属性

```
class StudentPerson extends Person {
    constructor(x, y, name) {
        super(x ,y) //调用父类的constructor(x, y)
        this.name = name
    }
    
    toSayhi() {
    	// super.父类方法  调用父类方法 this指向当前子类的实例
    	return super.toSayHello()
    }
}
```

#### 类的protype属性(原型对象)和__proto__属性

- Class作为构造函数的语法糖,同时有**prototype**属性和**proto**属性
- 每一个对象都有**proto**属性,指向对应的构造函数的**prototype**属性
- 子类proto属性,表示构造函数的继承,总是指向父类
- 子类prototype属性的proto属性,表示方法的继承,指向父类的prototype属性

#### 实例的__proto__属性

子类实例的**proto**属性的**proto**属性,指向父类实例的**proto**属性

#### 原型链

只要是对象就有原型, 并且原型也是对象, 因此只要定义了一个对象, 那么就可以找到他的原型, 如此反复, 就可以构成一个对象的序列, 这个结构就被成为**原型链** 最顶端是 Object对象