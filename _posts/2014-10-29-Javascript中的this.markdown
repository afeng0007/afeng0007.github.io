---
---

#### Javascript中this的用法：

1. 纯粹的函数调用：
```
function test(){
    this.x = 1;
    alert(this.x);
}
```
这个代码中this指向全局对象Global。
如下的代码中this也是指向global
```
x = 1;
function test(){
    alert(this.x);
}
```

2. 作为对象方法调用：
此时this指向这个上级对象。
```
function test(){
    alert(this.x);
}
var o = {};
o.x = 1;
o.m = test;
o.m();
```

3. 作为构造函数调用：
```
function test(){
    this.x = 1;
}
var o = new test();
alert(o.x);
```

4. apply调用：
```
var x = 0;
function test(){
    alert(this.x);
}
var o = {};
o.x = 1;
o.m = test;
o.m.apply();
o.m.apply(o);
```
