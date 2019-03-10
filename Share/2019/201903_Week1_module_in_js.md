
# JavaScript中模块化的几种方案

## IIFE和命名空间

早期通过全局的变量定义一个命名空间进行模块化的封装，这种方法其实是一种hack，对对象的一种特殊使用。而
IIFE(立即执行表达式)则是利用函数的作用域来进行模块化的封装。

## Commonjs和AMD(Asynchronous module definition)

经过Nodejs的推进，Commonjs逐渐流行起来，简单好用的语法，容易让人接受，不过较大的弊端是其只能同步引入，导致在web端无法很好的使用。而AMD(Asynchronous module definition)则是为web端的异步加载而创造
的，缺点是语法看起来略复杂。

## ES6 module

ES标准则从Commonjs和AMD中吸取各自的有点优点，并使用import语法引入到ES6标准中。