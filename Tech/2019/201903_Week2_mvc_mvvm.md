
有关MVC和MVVM的理解，读了一些文章，但是理解还不够深，有必要继续深挖一下

## 对MVC和MVVM的理解

先记录一下目前的理解:

### 基本概念

MVC: Model, View, Controller

MVVM: Model, View, ViewModel

其中Model指的是数据，关联到后端，在实行前后端分离的情况下，主要涉及后端持久化相关的数据；View指的是展示层，也就是页面；
MVC和MVVM最大的差别就在于C和VM，如何去连接View和Model。

### 差异

MVC中的Controller做的事情是，把所有的逻辑集合在一起，从页面到数据以及数据到页面展示，这里的一个弊端就是，页面复杂的情况下，
Controller会变得臃肿庞大。

MVVM中ViewModel则是将范围扩大了，直接涉及到页面层面，并形成一个虚拟的DOM，用以比对和更新实际的页面。页面是可以直接和后端
进行交互获取数据的。

### 遗留

* 两者的优势和劣势
* 两者的应用场景
* 未来的趋势

## 参考文章

[MVC vs. MVVM: How a Website Communicates With Its Data Models](https://hackernoon.com/mvc-vs-mvvm-how-a-website-communicates-with-its-data-models-18553877bf7d)