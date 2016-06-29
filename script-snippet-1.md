
## 原型相关代码
```javascript
function Person(){

}

Person.prototype.name = 'Nicholas';
Person.prototype.age = 29;
Person.prototype.job = 'Software Engineer';
Person.prototype.sayName = function(){
    console.log(this.name);
}

var person1 = new Person();
person1.sayName(); // 'Nicholas'

var person2 = new Person();
person2.sayName(); // 'Nicholas'

console.log(person1.sayName === person2.sayName);// true
console.log(Person.prototype.isPrototypeOf(person1)); // true

console.log(Object.getPrototypeOf(person1).name); // 'Nicholas'
console.log(Object.getPrototypeOf(person1) == Person.prototype); // true

console.log(Object.keys(Person.prototype)); // ["name", "age", "job", "sayName"]
console.log(Object.keys(person1)); // []

console.log(Object.getOwnPropertyNames(Person.prototype)) //["constructor", "name", "age", "job", "sayName"]
console.log(Object.getOwnPropertyNames(person1)) // []
```

## 原型模式缺点
```javascript
function Person(){

}

Person.prototype = {
  constructor : Person,
  name : 'Nicholas',
  age : 22,
  job : 'Software Engineer',
  friends : ['Shelby','Court'],
  sayName : function(){
    console.log(this.name);
  }
}

var person1 = new Person();
var person2 = new Person();

person1.friends.push('Van');

console.log(person1.friends); // ["Shelby", "Court", "Van"]
console.log(person2.friends); // ["Shelby", "Court", "Van"]

console.log(person1.friends == person2.friends); // true
```
