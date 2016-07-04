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
  return o;
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

```javascript
function Person(){

}

Person.prototype = {
  name : 'Nicholas',
  age : 22,
  job : 'Software Engineer',
  sayName : function(){
    alert(this.name)
  }
}

// 重设构造函数，只适用于ECMAScript 5 兼容的浏览器
Object.defineProperty(Person.prototype, 'constructor',{
  enumerable : false,
  value : Person
})

```
4. 组合使用构造函数模式和原型模式
```javascript
function Person(name, age, job){
  this.name = name;
  this.age = age;
  this.job = job;
  this.friends = ['Shelby', 'Court'];
}

Person.prototype = {
  sayName : function(){
    alert(this.name)
  }
}

Object.defineProperty(Person.prototype, 'constructor'{
  enumerable : false,
  value : Person
})

var person1 = new Person('Nicholas', 22, 'Software Engineer')
var person2 = new Person('Greg', 27, 'Doctor')

person1.friends.push('Van');
alert(person1.friends); // 'Shelby,Court,Van'
alert(person1.friends); // 'Shelby,Court'
alert(person1.friends == person2.friends); // false
alert(person1.sayName == person2.sayName); // true
```
5. 动态原型模式
```javascript
function Person(name, age, job){
  // 属性
  this.name = name;
  this.age = age;
  this.job = job;

  // 方法
  if(typeof this.sayName != 'function'){
    Person.prototype.sayName = function(){
      alert(this.name);
    }
  }
}

var friend = new Person('Nicholas', 29, 'Software Engineer');
friend.sayName();
```
6. 寄生构造函数模式
```javascript
function Person(name, age, job){
  var o = new Object();
  o.name = name;
  o.age = age;
  o.job = job;
  o.sayName = function(){
    alert(this.name)
  };
  return o;
}

var friend = new Person('Nicholas', 22, 'Software Engineer');
friend.sayName(); // 'Nicholas'
```
7. 稳妥构造函数模式
```javascript
function Person(name, age, job){
  // 创建要返回的对象
  var o = new Object();

  // 可以在这里定义私有变量和函数


  // 添加方法
  o.sayName = function(){
    alert(name);
  }

  // 返回对象
  return o;
}

var friend = new Person('Nicholas', 22, 'Software Engineer');
friend.sayName();

```

















 
