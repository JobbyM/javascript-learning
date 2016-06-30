## 创建对象
1. 工厂模式
```javascript
function createPerson(name, age, job){
  var o = new Object();
  o.name = name;
  o.age = age;
  o.job = job;
  o.sayName = function(){
    alert(this.name)
  }
}

var person1 = createPerson('Nicholas', 29, 'Software Engineer');
var person2 = createPerson('Greg', 27, 'Doctor');
```
2. 构造函数模式
```javascript
function Person(name, age, job){
  this.name = name;
  this.age = age;
  this.job = job;
  this.sayName = function(){
    alert(this.name);
  }
}
var person1 = new Person('Nicholas', 29, 'Software Engineer');
var person2 = new Person('Greg', 27, 'Doctor');

alert(person1.constructor == Person); // true
alert(person2.constructor == Person); // true

alert(person1 instanceof Object); // true
alert(person1 instanceof Person); // true
```
3. 原型模式
```javascript
function Person(){

}
Person.prototype.name = 'Nicholas';
Person.prototype.age = 22;
Person.prototype.job = 'Software Engineer';
Person.prototype.sayName = function(){
  alert(this.name)
}

var person1 = new Person();
person1.sayName(); // 'Nicholas'

var person2 = new Person();
person2.sayName(); // 'Nicholas'

alert(person1.sayName == person2.sayName); // true
```
4. 组合使用构造函数模式和原型模式
5. 动态原型模式
6. 寄生构造函数模式
7. 稳妥构造函数模式
