
## 创建对象的3种常见方法

### 对象字面量

```js
var obj = {
  name: "Nicolas",
  age: 28
};
```

### 构造函数

```js
function M(name) {
  this.name = name;
}

var obj = new M('James');
```

### Object.create

```js
var p = {
  name: "Nico",
  age: 30
};
var obj = Object.create(p);
```

## 原型链

用途:

通过原型链，各个对象可以进行层级的属性查找。 

## JavaScript中创建对象的7种方法(红宝书)

1. 工厂模式
2. 构造函数
3. 原型模式
4. 组合构造函数模式和原型模式
5. 动态原型模式
6. 寄生构造函数模式
7. 稳妥构造函数模式