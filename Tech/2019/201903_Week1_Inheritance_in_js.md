继承(通过原型链实现继承):
```
1. 构造函数继承方案，缺点为无法共享函数的定义
2. 原型继承方案，引用类型的属性会被共享以及无法实现参数初始化
3. 组合原型和构造继承
4. 原型式继承
5. 寄生式继承
6. 寄生组合式继承
```

```js
  // 原型链
  function SuperType() {
    this.property = true;
    this.colors = ["red", "blue", "green"];
  }
  SuperType.prototype.getSuperValue = function() {
    return this.property;
  };

  function SubType() {
    this.subproperty = false;
  }
  SubType.prototype = new SuperType();
  SubType.prototype.getSubValue = function() {
    return this.subproperty;
  };

  var instance = new SubType();
  instance.colors.push("black");
  console.log(instance.getSuperValue());
  console.log(instance.constructor);
  console.log(instance.colors);

  var instance2 = new SubType();
  console.log(instance2.colors);

  // 借用构造函数
  function SuperType1(name) {
    this.colors = ["red", "blue", "green"];
    this.name = name;
  }
  function SubType1() {
    SuperType1.call(this, "Nicholas");

    this.age = 29;
  }

  var instance3 = new SubType1();
  instance3.colors.push("black");
  console.log(instance3.colors, instance3.name, instance3.age);

  var instance4 = new SubType1();
  console.log(instance4.colors);

  // 组合继承
  function SuperType2(name) {
    console.log('call SuperType2 constructor');
    this.name = name;
    this.colors = ["red", "blue", "green"];
  }
  SuperType2.prototype.sayName = function() {
    console.log(this.name);
  };
  function SubType2(name, age) {
    SuperType2.call(this, name);
    this.age = age;
  }
  SubType2.prototype = new SuperType2();
  SubType2.prototype.sayAge = function() {
    console.log(this.age);
  };

  var instance5 = new SubType2("Nicholas", 29);
  instance5.colors.push("black");
  console.log(instance5.colors, instance5.sayName(), instance5.sayAge());

  var instance6 = new SubType2("Greg", 27);
  console.log(instance6.colors, instance6.sayName(), instance6.sayAge());

  // 原型式继承
  function object(o) {
    function F() {}
    F.prototype = o;
    return new F();
  }

  var person = {
    name: "Nicholas",
    friends: ["Shelby", "Court", "Van"]
  };

  var anotherPerson = object(person);
  anotherPerson.name = "Greg";
  anotherPerson.friends.push("Rob");

  var yetAnotherPerson = object(person);
  yetAnotherPerson.name = "Linda";
  yetAnotherPerson.friends.push("Barbie");

  console.log(person.friends);

  // 寄生式继承
  function createAnother(original) {
    var clone = object(original);
    clone.sayHi = function() {
      console.log("hi");
    };
    return clone;
  }

  var person1 = {
    name: "Nicholas",
    friends: ["Shelby", "Court", "Van"]
  };

  var anotherPerson1 = createAnother(person1);
  console.log(anotherPerson1.sayHi());

  // 寄生组合式继承
  function inheritPrototype(subType, superType) {
    var prototype = object(superType.prototype);
    prototype.constructor = subType;
    subType.prototype = prototype;
  }

  function SuperType3(name) {
    this.name = name;
    this.colors = ["red", "blue", "green"];
  }
  SuperType3.prototype.sayName = function() {
    console.log(this.name);
  };
  function SubType3(name, age) {
    SuperType3.call(this, name);

    this.age = age;
  }
  inheritPrototype(SubType3, SuperType3);

  SubType3.prototype.sayAge = function() {
    console.log(this.age);
  };

  var instance7 = new SubType3("a", 28);
  instance7.sayAge();
  console.log(instance7.name, instance7.age);
  console.log(instance7 instanceof SubType3, instance7 instanceof SuperType3);
```