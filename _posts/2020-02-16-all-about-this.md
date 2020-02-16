---
published: true
---
## All About This

This is always a confusing part in Javascript. MDN documentation says "In most cases, the value of this is determined by how a function is called (runtime binding)". That means this is not determined by where the function is written but how it is invoked.

1. The most basic case:
```
var myObject = {
	name: "Bruce Wayne",
  	getName: function () {
    	return this.name;
  	}
};
```
```
myObject.getName(); //Bruce Wayne
```


2. Object within Objewct
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

3. Destructured method

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

4. The arrow function
```
var name = "Global Name";

var myObject = {
	name: "Bruce Wayne",
  getName: () => {
    return this.name;
  }
};

myObject.getName();
```
