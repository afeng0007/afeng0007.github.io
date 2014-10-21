---
layout: post
title:  "coffee-script读书笔记"
date:   2014-10-21 15:01:00
categories: 读书笔记
---

#### 简介：   
coffee-script是能够将编写的代码直接转换成javascript的中间语言，和coffee-script类似的还有microsoft的type-script. 
#### Javascript的不足：
javascript因为历史的原因有以下的遗留问题：
    a. 比较奇怪的继承机制：Javascript在出现的最初是没有面向对象的。javascript因为这个原因并不是原生面向对象的，而是通过比较奇怪的原型链的方式进行继承。使用coffee-script可以比较容易进行继承。   
    b. Javascript编写起来比较繁琐：因为Javascript被设计成为单线程操作。在实现同一个方法会有非常多的回调函数来处理。因此编写Javascript会比较费事。coffeescript对Javascript中比较繁琐的部分进行了简化。使用coffeescript可以提高编码效率。   
    c.Javascript本身是弱类型的语言，这样就很难在编码阶段及时发现编码中存在的问题。只有经过充分的测试才能保证代码的正确性，这样就比强类型语言更容易出错。而有的中间语言（type-script）可以进行编码检查。这样就基本保证了编码的正确性，但是coffeescript并没有这样的类型检查功能。   

#### coffee-script的语法：   
a. 函数：函数通过一组可选的圆括号包裹的参数，一个箭头，一个函数体来定义。一个典型的函数。

{% highlight coffee %}
square = (x) -> x * x
{% endhighlight %}
    
一些函数参数会有默认值：当有默认值的时候定义为:
    
{% highlight coffee %}
    fill = (container, liquid = "coffee") ->
        "Filling the #{container} with #{liquid}..."
{% endhighlight %}
    
b. 对象和数组：Coffeescript中对象和数组的字面量看起来很像JavaScript中的写法。   
c. 词法作用域和变量安全：coffee-script会考虑所有变量，保证每个变量都在词法域中被适当的定义，永远都不需要自己写var。   
d. if, else, unless和条件赋值：if else 表达式可以不用圆括号和花括号就写出来，就像其他函数和块级表达式一样。多行的条件可以通过缩进来表明。coffeescript中没有三元表达式，可以在同一行内使用普通的if。   
    
{% highlight coffee %}
    date = if friday then sue else jill
{% endhighlight %}
    
e. 变参：可以使用以下的方法来提供变参语法。

{% highlight coffee %}
    awardMedals = (first, second, others...) ->
        gold   = first
        silver = second
        rest   = others
{% endhighlight %}
f.循环和推导式：你可以使用coffeescript将大多数循环写成基于数组，对象或者范围的推导式，推导式替代for循环，并且可以使用可选之句和数组索引值。推导式是表达式可以被循环和赋值。   
g. 数组边界和范围边界：范围能用来确定数组的边界。比如两个点(..)可以用来确定一个前闭后闭的边界，三个点可以用来确定一个前闭后开的边界。相同的语法能用来赋值或者替换。   
h. 操作符和别名：is 对应 ===, isnt 对应 !==, not 对应 !, and 对应 &&，or 对应 ||, true, yes, on 对应 true. false off no 对应 false, @ this 对应 this。of 对应 in, in 在javascript中没有对应. a**b 对应Math.pow(a, b), a // b 对应 Math.floor(a/b); a%%b 对应 (a%b + b) % b.   
