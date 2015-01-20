---
---

#### Great Features in ECMAScript6

##### classes:
In the Javascript version before, you can define a object by this:
```
function Car(make){
    this.make=make;
    this.currentSpeed=25;
    this.printCurrentSpeed=function(){
        console.log(this.make + ' is going ' + this.currentSpeed + " mph.");
    }
}
```

In the ECMAScript6, it support to define a class like other language:
```
class Car{
    constructor(make){
        this.make = make;
        this.currentSpeed=25;
    }
    printCurrentSpeed(){
        console.log();
    }
}

class RaceCar extends Car{
    constructor(make, topSpeed){
        super(make);
        this.topSpeed=topSpeed;
    }
}
```

##### Arrow Functions:
In the ECMAScript before, you have to define like this:
```
function Car(){
    var self = this;
    self.speed = 0;
    setInterval(function goFaster(){
        self.speed += 5;
        console.log();
        }, 1000);
}
```
In the ECMAScript6, you can define like this:
```
function Car(){
    this.speed = 0;
    setInterval(() => {
        this.speed += 5;
        console.log();
        }, 1000);
}
```

##### Modules:

##### Block Scoping:

##### Promoses:

#### ECMAScript6的新特性：
1. let命令：

2. const命令: const 用来声明不会发生变化的常量.

3. set数据结构：类似于数组，但是成员的值是唯一的。

4. map数据结构：类似于对象，就是一个键值对的集合，但是“键”的范围不限于字符串，对象也可以当作键。

5. rest(...)运算符:用于获取多余参数，这样就不需要使用arguments.length

6. 遍历器：遍历器协议规定，任意对象只要部署了next方法，就可以作为遍历器。但是next方法必须返回一个包含value和done两个属性的对象。

7. generator函数：

8. 原生对象的扩展：ES6对JavaScript的原生对象进行了扩展。提供了一系列的属性和方法：

#### 语法糖：







