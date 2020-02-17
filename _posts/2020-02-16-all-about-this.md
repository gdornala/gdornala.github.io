---
published: true
---
This is always a confusing part in Javascript. MDN documentation says "In most cases, the value of this is determined by how a function is called (runtime binding)". That means this is not determined by where the function is written but how it is invoked.

**The most basic case:**
```
var myObject = {
	name: "Bruce Wayne",
  	getName: function () {
    	return this.name;
  	}
};
myObject.getName(); //Bruce Wayne
```


**Object within Object**
```
var parentObject = {
	name: "Bruce Wayne",
    childObject: {
    	name: "Joker",
    	getName: function () {
     		return this.name;
    	}
  	}
};
parentObject.getName(); // "Bruce Wayne"
parentObject.childObject.getName(); //"Joker"
```

**Destructured method**

```
var name = "Global Name";
var myObject = {
	name: "Bruce Wayne",
  	getName: function () {
    	return this.name;
    }
};
var {getName} = myObject;
getName(); // "Global Name"
```

**The fat arrow function**

```
var name = "Global Name";
var myObject = {
	name: "Bruce Wayne",
	getName: () => {
    	return this.name;
  	}
};
myObject.getName(); // "Global Name";
```
**Explicit binding**

```
var name = "Global Name";
var myObject = {
	name: "Bruce Wayne",
	getName: function {
    return this.name;
  }
};

myObject.getName.call({name: "New Name}); // New Name
```
Explicit binding took precedence over invoking context

**Explicit Binding with Arrow Function**
```
var name = "Global Name";
var myObject = {
	name: "Bruce Wayne",
	getName: () => {
    return this.name;
  }
};
myObject.getName.call({name: "New Name"}); // "Global Name"
```
Here arrow function took precedence over explisit binding.

**this in constructor invoked with new**
```
function User(name, age) {
  this.name = name,
  this.age = age,
};
var myUser = new User();
```

When a constructor is invoked with "new" operator, it creates a new object. Usually the constructor modifies the object and the function returns "this" (which is the newly formed object).

**React class method without explicit binding**


In React we know that we have to bind the class method in its constrctor. What if we do not bind? React ensures that the method sets undefined rather than global name.

**React with arrow function method**

When arrow function is used for a method instead of regular function that is binded in constructor, React defines the method on it's constructor instead of it's prototype function. What exactly it means?

It means that the method is on every instance of the class instead of the constructor's prototype. It might cause some issues in testing with mock data. 

**static method of class**

Static methods do not belong to any specific instance but for the class itself. So this in static method points to the class itself.

```
Class MyClass {
  static myStaticMethod() {
    console.log(this === Class);
  }
}
MyClass.myStaticMethod(); // true
```

> Ref: 
https://medium.com/@charpeni/arrow-functions-in-class-properties-might-not-be-as-great-as-we-think-3b3551c440b1
https://dev.to/taesup/all-about-this-in-javascript-30j
