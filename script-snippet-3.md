
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

3. 组合继承

```javascript
function SuperType(name){
  this.name = name;
  this.colors = ['red','blue','green']
}

SuperType.prototype.sayName = function(){
  alert(this.name)
}

function SubType(name, age){
  // 继承属性
  SuperType.call(this, name);

  this.age = age;
}

// 继承方法
SubType.prototype = new SuperType();

SubType.prototype.sayAge = function(){
  alert(this.age)
}

var instance1 = new SubType('Nicholas', 22)
instance1.colors.push('black')
alert(instance1.colors) //["red", "blue", "green", "black"]
instance1.sayName(); // 'Nicholas'
instance1.sayAge(); // 22

var instance2 = new SubType('Greg',19)
alert(instance2.colors); // ["red", "blue", "green"]
instance2.sayName(); // 'Greg'
instance2.sayAge(); // 19
```
4. 原型式继承

```javascript
function object(o){
  function F(){};
  F.prototype = o;
  return new F();
}

var person = {
  name : 'Nicholas',
  friends : ['Shelby', 'Court', 'Van']
}

var anotherPerson = object(person);
anotherPerson.name = 'Greg';
anotherPerson.friends.push('Rob');

var yetAnotherPerson = object(person);
yetAnotherPerson.name = 'Linda';
yetAnotherPerson.friends.push('Barbie');

alert(person.friends); // ["Shelby", "Court", "Van", "Rob", "Barbie"]
```

```javascript
var person = {
  name : 'Nicholas',
  friends : ['Shelby', 'Court', 'Van']
}

var anotherPerson = Object.create(person);
anotherPerson.name = 'Greg';
anotherPerson.friends.push('Rob');

var yetAnotherPerson = Object.create(person);
yetAnotherPerson.name = 'Linda';
yetAnotherPerson.friends.push('Barbie');

alert(person.friends); // ["Shelby", "Court", "Van", "Rob", "Barbie"]
```
5. 寄生式继承

```javascript
function object(o){
  function F(){}
  F.prototype = o;
  return new F();
}

function createAnother(original){
  var clone = object(original); // 通过调用函数创建一个新对象
  clone.sayHi = function(){   // 以某种方式来增强这个对象
    alert('hi');
  };
  return clone;               // 返回这个对象
}

var person = {
  name : 'Nicholas',
  friends : ['Shelby', 'Court', 'Van']
}

var anotherPerson = createAnother(person);
anotherPerson.sayHi(); // 'hi'
```

6. 寄生组合式继承

```javascript
function object(o){
  function F(){}
  F.prototype = o;
  return new F();
}

function inheritPrototype(subType, superType){
  var prototype = object(superType.prototype); // 创建对象
  prototype.constructor = subType;             // 增强对象
  subType.prototype = prototype;               // 指定对象
}

function SuperType(name){
  this.name = name;
  this.colors = ['red', 'blue', 'green'];
}

SuperType.prototype.sayName = function(){
  alert(this.name)
}

function SubType(name, age){
  SuperType.call(this, name);
  this.age = age;
}

inheritPrototype(SubType, SuperType)

SubType.prototype.sayAge = function(){
  alert(this.age)
}

var instance = new SubType('Nicholas', 22);
instance.sayName(); // 'Nicholas'
instance.sayAge(); // '22'
``` 











 
