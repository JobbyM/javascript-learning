## 继承

1. 原型链
```javascript
function SuperType(){
  this.property = true;
}

SuperType.prototype.getSuperValue = function(){
  return this.property;
}

function SubType(){
  this.subproperty = false;
}

// 继承了 SuperType
SubType.prototype = new SuperType();

SubType.prototype.getSubValue = function(){
  return this.subproperty;
}

var instance = new SubType();
alert(instance.getSuperValue()); // true

alert(instance instanceof Object); // true
alert(instance instanceof SuperType); // true
alert(instance instanceof SubType); // true

alert(Object.prototype.isPrototypeOf(instance)); // true
alert(SuperType.prototype.isPrototypeOf(instance));// true
alert(SubType.prototype.isPrototypeOf(instance)); // true

```

2. 借用构造函数（constructor stealing）（伪造对象或经典继承）
```javascript
function SuperType(){
  this.colors = ['red','blue','green']
}

function SubType(){
  // 继承了SuperType
  SuperType.call(this)
}

var instance1 = new SubType();
instance1.colors.push('black');  
alert(instance1.colors); //["red", "blue", "green", "black"]

var instance2 = new SubType();
alert(instance2.colors); // ["red", "blue", "green"]
```

```javascript
function SuperType(name){
  this.name = name;
}

function SubType(){
  // 继承了SuperType，同时还传递了参数
  SuperType.call(this, 'Nicholas');

  // 实例属性
  this.age = 22;
}

var instance = new SubType();
alert(instance.name); // 'Nicholas'
alert(instance.age); // 22
```
