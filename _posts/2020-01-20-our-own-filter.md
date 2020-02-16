---
layout: post
title: Your own Filter
published: true
---

Ever wondered how we can implemented our own filter function that does the same as filter() on Array prototype? Let us try to write one:

First let us see what a filter does. filter() method takes a callback function. That callback gets executed for each of the array's elements. If callback returns true, that element gets added to the result, otherwise it would be skipped.

For example let us say I have an array like this.
```
const myArray = ["a", "b", "c"];
```

and if I use filter like the following code,

```
myArray.filter((element, index) => {
	if (element === "a") {
    return false;
  }
  return true;
});
```

it would return a new array like this ["b", "c"];

So what exactly is happening? 1. filter function is taking a callback function 2. it is invoking that callback for every element with arguments as element, index and array and returning a filtered array to us.

Now let us try to implement the same in our own method.

## Step 1

Add a method myFilter on Array's prototype. It should take a callback function as argument and return new array;

```
Array.prototype.myFilter = function (callback) {
  const newArray = [];
  //rest of the logic
  return newArray;
}
```
    
## Step 2
The callback function should be triggered for each and every element of the array with element, index and array as arguments;

```
Array.prototype.myFilter = function (callback) {
	const newArray = [];
    for (let index = 0; index < this.length; index++) {
      callback(this[index], index, this);
      //logic to filter
    }
    return newArray;
}
```
    
## Step 3

Our method should return array with elements for those the callback function returns true.

```
Array.prototype.myFilter = function (callback) {
	const newArray = [];
  for (let index = 0; index < this.length; index++) {
    if (callback(this[index], index, this)) {
      newArray.push(this[index]);
    }
  }
  return newArray;
};
```
        
 Thats it. Now our own filter is ready.
