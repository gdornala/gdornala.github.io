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
**Explisit binding**

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
Explicist binding took precedence over invoking context

**Explisit Binding with Arrow Function**
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





