---
published: true
---
**Basic Constructor**
```
var User = function(name, age) {
	this.name = name,
    this.age = age;
    var getName = function() {
    	return this.name;
    }
}
var newUser = new User();
```
This pattern contains two problems:
1. It is hard to have inheritance
2. The code of methods is shared across all the user Objects.

**Constructor Prototype**
If we move method getName out of the constructor onto prototype, then the code of getName is shared across all its objects.

```
var User = function(name, age) {
	this.name = name,
	this.age = age;
};

User.prototype.getName = function() {
	return this.name;
}
var newUser = new User();
```
Now the objects of User share the methods.

**Inheritance with constructor prototype (pseudo classical inheritance)**
```
var AdminUser = function(name, age) {
	this.name = name;
    this.age = age;
};
AdminUser.prototype = new User();
```
We have changed AdminUser's prototype with new User(). It makes all the methods and properties available on User() automatically available to AdminUser objects.

The problems with this approach are:
1. There is no private data
2. If someone forgets to put new before constructor, it would overwrite global properties.

**Prototypal Inheritance**

In prototypal inheritance objects are created from a model object or prototype. It is different from classical inheritance in which there is no class, objects are created just from another object.

```
var carProto = {
 steering: 1,
 wheels: 4
 };
var myCar = Object.create(carProto)
```
In myCar can get new properties defined as second argument to Object.create().


