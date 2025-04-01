# All_POLYFILLS_JS

 ### Polyfills:-Means Most of the old browsers don't support inbuilt functions so we need to write   that function in an imperative way so that they can support the browser.

## Array Polyfills -
* #### Array.map method on Array prototype
* #### Array.filter method on the Array Prototype
* #### Array.forEach method on the Array Prototype
* #### Array.find method on the Array Prototype
* #### Array.findIndex method on the Array Prototype
* #### Array.reduce method on the Array Prototype
* #### Array.some method on the Array Prototype
* #### Array.every method on the Array Prototype
* #### Array.flat method (that will flatten an array into a 1D array) Array Prototype
* #### Array.slice method
* #### Array.splice method
* #### Array.forIn  method
* #### Array.forOf method

## Function Polyfills-

* #### Implement Function.bind using call/apply (DONE)
* #### Implement Function.apply using call (DONE)
* #### Implement Function.call using apply (DONE)

## Promise Polyfills / Async Helpers-

* #### Implement Async.sequence, which chains up async functions, like what pipe() does
* #### Implement Async.parallel, which executes a set of async tasks parallely
* #### Implement Async.series, which executes a set of async tasks in series
* #### Write a method that will implement Promise.all
* #### Write a method that will implement Promise.race
* #### Write a method that will implement Promise.finally
* #### Write a method that will implement Promise.any
* #### Implement Promisify, provide promise support to function perform asynchronous tasks
* #### Implement Promise class

## JS Problems -
* #### Implement SetInterval Polyfill using setTimeout (DONE)
* #### Implement debounce
* #### Implement throttle
* #### Write a function memoize(memo) that will subsequent calls to a function
* #### Implement clearAllTimeout
* #### Implement an Event Emitter class
* #### Implement deep equal _.isEqual()
* #### Map class
* #### Set class
* #### Event bubbling and Event Capturing
* #### Event Delegation ,Method chaining
  ---  

  ### Before Starting we need to undertand Higher order function
  ## Higher Order Function

 #### In JavaScript, functions are treated as first-class citizens. We can treat functions as values and assign them to another variable, pass them as arguments to another function, or even return them from another function
#### This ability of functions to act as first-class functions is what powers higher order functions    in JavaScript.
#### Basically, a function which takes another function as an argument or returns a function is known as a higher order function.
#### We know that JavaScript provides us with some inbuilt higher order functions like map(), filter(), reduce() and so on.


## 🚀Map()  =>

* ### The map() method is a built-in JavaScript function that creates a new array by applying a callback function to each element of an existing array.

* ### 👉 It does NOT modify the original array; instead, it returns a new array with transformed values.

```js
             const numbers = [1,2,3, 4];
             const newArr = numbers.map(function(num) {
             return num *num;
               }
              )
            
          Output:[1,4,9,16]
```
## Prototype Polyfills of map() :-
```js
       // Adding a custom map method to the Array prototype
Array.prototype.myMap = function(callback) {
    // Create a new array to store transformed elements
    let newArr = [];
    
    // Iterate over the array using `this` (refers to the array calling `myMap`)
    for (let i = 0; i < this.length; i++) {
        // Push the result of applying the callback function to the current element
        newArr.push(callback(this[i], i, this));  
        // The callback receives three arguments: 
        // - this[i]  → current element
        // - i        → current index
        // - this     → the whole array
    }
    
    // Return the new array after transformation
    return newArr;
};

// Callback function that squares a number
function square(x) {
    return x * x;
}

// Test array
let myArr = [1, 2, 3, 4];

// Using the custom myMap function
let mappedArr = myArr.myMap(square);

// Output the result
console.log(mappedArr);  // [1, 4, 9, 16]

```
--- 


## 🚀filter()  =>
The `filter()` method is used to create a new array containing only elements that satisfy a given condition.

👉 Unlike `map()`, which transforms elements, `filter()` only includes elements that return true in the callback function.

### ✅ Syntax:
```js
array.filter(callback(currentValue, index, array))
```
### 🛠 Parameters:
* #### callback → Function that runs for each element.
* #### currentValue → The current element being processed.
* #### index (optional) → The index of the current element.
* #### array (optional) → The original array.
* #### Returns: A new array with elements that satisfy the condition.

```js
const ages = [32, 33, 16, 40];

const result = ages.filter(age => age >= 18);

console.log(result);  // [32, 33, 40]
```

## 📌 Polyfill for filter() (Custom Implementation)
```js
// Adding a custom filter method to the Array prototype
Array.prototype.myFilter = function(callback) {
    let newArr = []; // Create a new array to store filtered elements
    
    // Iterate over the array using `this`
    for (let i = 0; i < this.length; i++) {
        if (callback(this[i], i, this)) {  
            // If callback returns true, push the element into newArr
            newArr.push(this[i]);
        }
    }
    
    // Return the new array after filtering
    return newArr;
};

// Callback function to check if a number is even
function isEven(x) {
    return x % 2 === 0;
}

// Test array
let myArr = [1, 2, 3, 4];

// Using the custom myFilter function
let filteredArr = myArr.myFilter(isEven);

console.log(filteredArr);  // [2, 4]
```
## 🎯 Key Takeaways
* #### ✔ filter() creates a new array with elements that match a condition.
* #### ✔ Does NOT modify the original array.
* #### ✔ Returns a new array that may be smaller than the original.
* #### ✔ Works well with arrays of numbers, strings, or objects.
* #### ✔ Custom Polyfills can be created using Array.prototype.
  ---

## 🚀Reduce ()=>
#### The reduce() method is used to accumulate values from an array into a single output value by applying a function to each element.

#### 👉 Unlike map() and filter(), which return arrays, reduce() returns a single value (e.g., sum, product, concatenation, or even an object).
## ✅ Syntax:
```js
array.reduce(callback(accumulator, currentValue, index, array), initialValue)
```
## 🛠 Parameters:
* #### callback → A function that runs on each element.
* #### accumulator → The accumulated result from previous iterations.
* #### currentValue → The current element being processed.
* #### index (optional) → The index of the current element.
* #### array (optional) → The original array.
* #### initialValue (optional but recommended) → The starting value for accumulator.

* #### Returns: A single value (number, string, object, etc.).
## Example Sum of Numbers
```js
const numbers = [1, 2, 3, 4];

const sum = numbers.reduce((accumulator, num) => accumulator + num, 0);

console.log(sum);  // 10
```
### Explanation:
* #### reduce() starts with 0 (initialValue).
* #### It adds each element to accumulator

## 📌 Polyfill for reduce() (Custom Implementation)
```js
// Adding a custom reduce method to the Array prototype
Array.prototype.myReduce = function(callback, initialValue) {
    let accumulator = initialValue !== undefined ? initialValue : this[0]; 
    let startIndex = initialValue !== undefined ? 0 : 1; 

    // Iterate over the array
    for (let i = startIndex; i < this.length; i++) {
        accumulator = callback(accumulator, this[i], i, this);
    }

    // Return the final accumulated result
    return accumulator;
};

// Callback function to sum numbers
const sumNumbers = (acc, curr) => acc + curr;

// Test array
const numbers = [1, 2, 3, 4];

// Using the custom myReduce function
const total = numbers.myReduce(sumNumbers, 0);

console.log(total);  // 10
```
---  

## 🚀Find() =>

### The find() method returns the first element in an array that satisfies a given condition.
### 👉 If no element matches, it returns undefined.
## ✅ Syntax:
```js
array.find(callback(currentValue, index, array))
```
## 🛠 Parameters:
* #### callback → A function that runs on each element.
* #### currentValue → The current element being processed.
* #### index (optional) → The index of the current element.
* #### array (optional) → The original array.

* #### Returns: The first matching element or undefined if no match is found.

## Example 1: Finding the First Odd Number
```js
const numbers = [2, 4, 5, 6, 7, 9];

const firstOdd = numbers.find(num => num % 2 !== 0);

console.log(firstOdd);  // 5
```
### Explanation:

* #### find() checks each element until it finds 5, which is the first odd number.

* #### The loop stops immediately after the first match.

## 📌 Polyfill for find() (Custom Implementation)

```js
// Adding a custom find method to the Array prototype
Array.prototype.myFind = function(callback) {
    // Iterate over the array using `this`
    for (let i = 0; i < this.length; i++) {
        if (callback(this[i], i, this)) {  
            return this[i];  // Return the first matching element
        }
    }
    return undefined; // Return undefined if no match found
};

// Callback function to check if a number is odd
const isOdd = num => num % 2 !== 0;

// Test array
const numbers = [2, 4, 5, 6, 7, 9];

// Using the custom myFind function
const firstOdd = numbers.myFind(isOdd);

console.log(firstOdd);  // 5
```
---  

## 🚀findIndex() =>
### The findIndex() method returns the index of the first element in an array that satisfies a given condition.
### 👉 If no element matches, it returns -1 instead of undefined (like find() does).
## ✅ Syntax:
```js
array.findIndex(callback(currentValue, index, array))
```
## 🛠 Parameters:
* #### callback → A function that runs on each element.
* #### currentValue → The current element being processed.

* #### index (optional) → The index of the current element.

* #### array (optional) → The original array.

* #### Returns: The index of the first matching element or -1 if no match is found.
## Example 1: Finding the Index of a Specific Number

```js
const numbers = [1, 2, 5, 3, 4, 5, 6];

const firstIndex = numbers.findIndex(num => num === 5);

console.log(firstIndex);  // 2
```
### Explanation:

* #### The first occurrence of 5 is at index 2, so findIndex() returns 2.

* #### The search stops immediately after the first match.
## 📌 Polyfill for findIndex() (Custom Implementation)
```js
// Adding a custom findIndex method to the Array prototype
Array.prototype.myFindIndex = function(callback) {
    // Iterate over the array using `this`
    for (let i = 0; i < this.length; i++) {
        if (callback(this[i], i, this)) {  
            return i;  // Return the first matching index
        }
    }
    return -1; // Return -1 if no match is found
};

// Callback function to check if a number equals 5
const isFive = num => num === 5;

// Test array
const numbers = [1, 2, 5, 3, 4, 5, 6];

// Using the custom myFindIndex function
const firstIndex = numbers.myFindIndex(isFive);

console.log(firstIndex);  // 2
```
---  
## 🚀forEach() =>
The forEach() method is a higher-order function that iterates through each element of an array and executes a callback function once for each element.  

✅ Syntax:  

```js
array.forEach(callback(currentValue, index, array))
```
🛠 Parameters:
* #### callback: A function that is called for each element in the array.

* #### currentValue: The current element being processed.

* #### index (optional): The index of the current element.

* #### array (optional): The original array.

* #### Returns: undefined (no new array is created).

 ## Example - Displaying Todos
```js
const todos = [
  { id: 1, todo: "Morning Walk" },
  { id: 2, todo: "Go to Office" },
  { id: 3, todo: "Watch Netflix" },
  { id: 4, todo: "Go to Gym" },
  { id: 5, todo: "Go for Movie" },
];

const display = ({ todo }, index, array) => {
  console.log(todo);
};

todos.forEach(display);
```

### Output:

```js
Morning Walk
Go to Office
Watch Netflix
Go to Gym
Go for Movie
```
## Key Insights:
* #### forEach() executes the callback for each element in the array.

* #### Does NOT mutate the original array.

* ### Always returns undefined and does NOT create a new array (unlike map()).

## forEach() vs map():
* #### map() returns a new array, whereas forEach() always returns undefined.

* #### When to use map()?: Use it when you need to transform an array and return a new one (e.g., editing a todo list).

* #### When to use forEach()?: Use it when you simply want to loop through each element and perform an action without needing a new array (e.g., displaying a list of todos).

## 📌 Polyfill for forEach() (Custom Implementation)
```js
// Adding a custom forEach method to the Array prototype
Array.prototype.customForEach = function(callback) {
  // Iterate over the array using `this` (refers to the calling array)
  for (let i = 0; i < this.length; i++) {
    // Apply the callback to each element
    callback(this[i], i, this);
  }
};

// Callback function to display todo items
const display = ({ todo }, index, array) => {
  console.log(todo);
};

// Using the custom forEach function
todos.customForEach(display);
```
---  

## 🚀For-of():-

* #### Purpose: Iterates over iterable objects, such as arrays, strings, maps, sets, and more.
* #### Iterates Over: The values of the iterable object.
* #### Best Used For: Iterating through the contents (values) of arrays, strings, or other iterable objects.
```js
const arr = [10, 20, 30];


for (const value of arr) {
  console.log(value); // Output: 10, 20, 30
}

const str = "hello";
for (const char of str) {
  console.log(char); // Output: h, e, l, l, o
}
```
---  

## 🚀For-in():-
* #### Purpose: Iterates over the enumerable properties of an object.
* #### Iterates Over: The keys (property names) of an object or array indices.
* #### Best Used For: Iterating through object properties. It can also work with arrays but is not recommended because it iterates over all enumerable properties, not just array elements.
```js
const obj = { a: 1, b: 2, c: 3 };


for (const key in obj) {
  console.log(key); // Output: a, b, c
}


const arr = [10, 20, 30];
for (const index in arr) {
  console.log(index); // Output: 0, 1, 2
  console.log(arr[index]); // Output: 10, 20, 30
}
```
---  

## 🚀Some()->

### The some() method tests whether at least one element in the array passes the test implemented by the provided callback function.


#### Returns:
* #### true if any element satisfies the condition.
* #### false if none of the elements satisfy the condition.


* #### 💡Note - It does not mutate the original array, and returns a Boolean value.
* #### 👉 One Level Up :- We can create our own custom some( Polyfill of some ), Check out the code below.👇

## 💡 Example - Check if a Number is Greater than 5
```js
const numbers = [1, 2, 3, 4, 5, 6];

const isGreaterThan5 = (value, index, array) => {
  return value > 5;
};

const result = numbers.some(isGreaterThan5);
console.log("result", result);  // true
```
## 📌 Polyfill for some() (Custom Implementation)
```js
// Adding a custom some method to the Array prototype
Array.prototype.customSome = function(callback) {
  // Iterate over the array using `this` (refers to the calling array)
  for (let i = 0; i < this.length; i++) {
    // If callback returns true for any element, return true
    if (callback(this[i], i, this)) {
      return true;
    }
  }
  return false;  // Return false if no element satisfies the condition
};

// Callback function to check if a number is greater than 5
const isGreaterThan5 = (value, index, array) => {
  return value > 5;
};


// Using the custom some function
const resultCustom = numbers.customSome(isGreaterThan5);
console.log("resultCustom", resultCustom);  // true
```
---  

## 🚀every() =>

### The every() method tests whether all elements in the array pass the test implemented by the provided callback function. 
### It returns true if every element satisfies the condition, otherwise, it returns false.

✅ Syntax:
```js
array.every(callback(currentValue, index, array))
```
## 🛠 Parameters:
* #### callback: A function that tests each element.

* #### currentValue: The current element being processed.

* #### index (optional): The index of the current element.

* #### array (optional): The original array.

* #### Returns: true if all elements satisfy the condition, otherwise false.

## 💡 Example - Check if All Numbers are Less Than 10
```js
const numbers = [1, 2, 3, 4, 5];

// Check if all numbers are less than 10
const allLessThanTen = numbers.every(num => num < 10);

console.log(allLessThanTen);  // Output: true
```

## Key Insights:
* #### every() returns true if every element in the array satisfies the provided condition.

* #### It stops iterating as soon as it finds an element that fails the condition (short-circuiting behavior).

* #### It does NOT modify the original array.

## 💡 Use Case:
* #### Validating an entire list: For example, checking if all items in an array meet a certain condition, such as whether all numbers are within a valid range.

## 📌 Polyfill for every() (Custom Implementation)
```js
// Adding a custom every method to the Array prototype
Array.prototype.customEvery = function(callback) {
  // Iterate over the array using `this` (refers to the calling array)
  for (let i = 0; i < this.length; i++) {
    // If callback returns false for any element, return false
    if (!callback(this[i], i, this)) {
      return false;
    }
  }
  return true;  // Return true if all elements satisfy the condition
};

// Callback function to check if a number is less than 10
const isLessThanTen = num => num < 10;

// Using the custom every function
const allLessThanTenCustom = numbers.customEvery(isLessThanTen);

console.log(allLessThanTenCustom);  // Output: true
```
---  
## 🚀Slice():-
* #### Purpose: Creates a shallow copy of a portion of an array into a new array without modifying the original array.
### Arguments:
* #### start (optional): The index at which to begin the extraction (inclusive).
* #### end (optional): The index at which to stop the extraction (exclusive).
* #### Returns: A new array containing the extracted elements.
* #### Does not modify the original array.

```js
const numbers = [1, 2, 3, 4, 5];


// Extract elements from index 1 to 3 (exclusive)
const slicedArray = numbers.slice(1, 3);


console.log(slicedArray); // Output: [2, 3]
console.log(numbers);     // Output: [1, 2, 3, 4, 5] (original array unchanged)
```
## 📌 Polyfill for slice() (Custom Implementation)
```js
// Adding a custom slice method to the Array prototype
Array.prototype.customSlice = function(start, end) {
  // If end is undefined, set it to the length of the array
  end = end !== undefined ? end : this.length;

  // Adjust negative indices to count from the end
  if (start < 0) start = this.length + start;
  if (end < 0) end = this.length + end;

  // Create a new array for the sliced elements
  let slicedArray = [];
  
  // Iterate over the array and push elements into the new array
  for (let i = start; i < end; i++) {
    slicedArray.push(this[i]);
  }

  return slicedArray;
};

// Using the custom slice function
const slicedArrayCustom = numbers.customSlice(1, 3);

console.log(slicedArrayCustom);  // Output: [2, 3]
```
---  

## 🚀Splice():-
### Purpose: Modifies an array by adding, removing, or replacing elements.
### Arguments:
* #### start: The index at which to begin changing the array.
* #### deleteCount (optional): The number of elements to remove.
* #### items (optional): Elements to add to the array at the start index.
* #### Returns: An array of the removed elements.
* #### Modifies the original array.
 ```js
const numbers = [1, 2, 3, 4, 5];


// Remove 2 elements starting from index 1, and add "10" and "20" in their place
const removedElements = numbers.splice(1, 2, 10, 20);


console.log(removedElements); // Output: [2, 3] (removed elements)
console.log(numbers);         // Output: [1, 10, 20, 4, 5] (modified array)

```
## 📌 Polyfill for splice() (Custom Implementation)
```js
// Adding a custom splice method to the Array prototype
Array.prototype.customSplice = function(start, deleteCount, ...items) {
  let removedElements = [];  // Array to store removed elements
  let newArray = [...this];  // Make a copy of the array to modify

  // If deleteCount is not provided, remove all elements from start to the end of the array
  deleteCount = deleteCount || newArray.length - start;

  // Store removed elements
  removedElements = newArray.slice(start, start + deleteCount);

  // Remove the elements from the array
  newArray.splice(start, deleteCount);

  // Insert new elements at the start index
  if (items.length > 0) {
    newArray.splice(start, 0, ...items);
  }

  // Return the array of removed elements
  return removedElements;
};

// Using the custom splice function
const numbers = [1, 2, 3, 4, 5];
const removedElementsCustom = numbers.customSplice(1, 2, 10, 20);

console.log(removedElementsCustom);  // Output: [2, 3]
console.log(numbers);                // Output: [1, 10, 20, 4, 5]
```
---  

## So this is All about Array methods and thier polyfills 

--- 

#  Function PolyFills:-

## 🚀Call()=>
* #### The call method is basically used to invoke the function with different this object.
* #### In JavaScript, this refers to an object. It depends on how we are calling a particular function.
* #### In the global scope, this refers to the global object window. Inside function also this refers to the global object window.
  
* #### In strict mode, when we use any function then this refers to undefined. In functions like call, this could refer to a different object. 
* #### With the help of the call method, we can invoke a particular function with different objects.
* #### Parameters: It takes two parameters:
* #### ObjectInstance: It is an object which we want to use explicitly
* #### Arguments: It is arguments that we want to pass to the calling function
* #### The main purpose of the call() method in js is to change the context of (this value) of a function when its invoked.
* #### It allows you to specify the object on which function is to be invoked, rather than relying on the usual calling context,
* #### This is useful in situations where you want reuse function with different objects or when you need to explicitly set context for a function
  
* #### Note:It accepts the arguments individually

```js
let p1 = {
  firstName: 'John',
  lastName: 'Smith'
};
let p2 = {
  firstName: 'Ann',
  lastName: 'Brown'
};
function sayWelcome(greeting) {
  console.log(greeting + ' ' + this.firstName + ' ' + this.lastName);
}
sayWelcome.call(p1, 'Welcome'); // Welcome John Smith
sayWelcome.call(p2, 'Welcome'); // Welcome Ann Brown
```


## 📌Prototype Polyfills of Call() :-

```js
let person = {
firstname: "Kirtesh",
lastname: "bansal"
}
let printName = function (country) {
console.log(this.firstname + " " + this.lastname + " from "
+ country);
}
//...args=> rest parameter means we can add multiple arguments
Function.prototype.mycall = function(obj={},...args){
// console.log(this); //this keyword is refers to the pritName function
if(typeof this !=="function"){
throw new Error("not callable")
}
obj.fn=this;
obj.fn(...args)
}
/*
Note: Applying mycall method to printName function so this
will be equal to printName inside mycall function as
printName is on the left side of the '.'
*/
printName.mycall(person, "India");
// Output:
// "Kirtesh bansal from India"
```
--- 

## 🚀Apply()=>

### The apply() method calls the function with a given this value and allows passing  in arguments as an array (or an array-like object).
```js
let p1 = {
  firstName: 'John',
  lastName: 'Smith'
};
let p2 = {
  firstName: 'Ann',
  lastName: 'Brown'
};
function sayWelcome(greeting) {
  console.log(greeting + ' ' + this.firstName + ' ' + this.lastName);
}
sayWelcome.apply(p1, ['Welcome'] ); // Welcome John Smith
sayWelcome.apply(p2, ['Welcome'] ); // Welcome Ann Brown
```

* #### it is useful when we are working with function that accepts a variable number of arguments Such As mathmatical function.
* #### let say you have array of numbers and you want to find the maximum number in array then we can use apply method

```js
let arr=[22,33,44,11,13,45,75,23,43,54];
let maxNumber=Math.max.apply(null,arr);
console.log(maxNumber);
```
### Note:It aceepts the arguments as an array.

 ## 📌Prototype Polyfills of Apply():-
```js
// Step 1: Define an object
let p1 = {
  firstName: "sachin", // Fixed typo from 'fistName' to 'firstName'
  lastName: "deshpande"
};


// Step 2: Define a function
let printName = function (country) {
  console.log(this.firstName + " " + this.lastName + " from " + country);
};


// Step 3: Custom implementation of 'apply'
Function.prototype.myApply = function (obj = {}, args = []) {
  // Check if 'this' is a function
  if (typeof this !== 'function') {
      throw new Error("Function.prototype.myApply - called on non-callable object");
  }
  // Check if args is an array
  if (!Array.isArray(args)) {
      throw new Error("Function.prototype.myApply - second argument must be an array");
  }
  // Assign the function to the provided object's property
  obj.fn = this;
  // Invoke the function with the given arguments
  obj.fn(...args);
  // Clean up: remove the added property to avoid side effects
  delete obj.fn;
};


// Step 4: Use the custom myApply method
printName.myApply(p1, ["India"]);
```
---  

## 🚀Bind()=>

### The bind() method returns a new function and allows passing in a this array and any number of arguments.

```js
let p1 = {
  firstName: 'John',
  lastName: 'Smith'
};


let p2 = {
  firstName: 'Ann',
  lastName: 'Brown'
};
function sayWelcome() {
  console.log('Welcome ' + this.firstName + ' ' + this.lastName);
}
let sayWelcomeJohn = sayWelcome.bind(p1);
let sayWelcomeAnn = sayWelcome.bind(p2);
sayWelcomeJohn(); // Welcome John Smith
sayWelcomeAnn(); // Welcome Ann Brown

```

## 📌Prototype Polyfills of Bind():-
```js
let person = {
firstname: "Kirtesh",
lastname: "bansal"
}
let printName = function (country) {
console.log(this.firstname + " " + this.lastname + " from "
+ country);
}
//...args=> rest parameter means we can add multiple arguments
Function.prototype.mybind = function(obj={},...args1){
if(typeof this !=="function"){
throw new Error("not callable")
}
obj.fn=this;
return function(...args2){
obj.fn(...args1,...args2)
}
}
let pritFun=printName.mybind(person);
pritFun("India");
// Output:
// "Kirtesh bansal from India"

```
---  

## 🚀Promises 
### Promise is an object that is used for handling asynchronous operations in JavaScript.

## 💡Promise has 4 states :-
* #### 👉 fulfilled: Action related to the promise succeeded (resolve) => result in .then().
* #### 👉 rejected: Action related to the promise failed (reject) => result in .catch().
* #### 👉 pending: Promise is still pending i.e. not fulfilled or rejected yet.
* #### 👉 settled: Promise has fulfilled or rejected => .finally().

## 💡 Promise Chaining :-
 ### Promise chaining allows you to chain together multiple asynchronous tasks in a specific order where one asynchronous task needs to be performed after the completion of other asynchronous task.

* #### 💡 We can perform Promise Chaining :-
* #### 👉 by returning a new instance of promise in then()
* #### 👉 by returning a value in then (), behind the scene it returns a new promise that immediately resolves to the return value.

## 💡 Benefits of Promises :-
* #### 👉 Improves Code Readability.
* #### 👉 Better handling of asynchronous operations.
* #### 👉 Better Error Handling.

https://www.youtube.com/watch?v=PL2D7u64M84
Watch this video for Promises

## Example of Promise:-
```js
const myPromise = new Promise((resolve, reject) => {
      setTimeout(()=>{
        const randomNumber = Math.random()
        if(randomNumber < 0.5){
             resolve(randomNumber)
        }else{
             reject("Operation failed")
        }
      },500)
  })
  myPromise.then((result)=>{
      console.log("SUCCESS:",result)
  }).catch(err=>{
      console.log("ERROR:",err)
  })
```

## 📌Prototype Polyfills of promise:-
```js
class MyPromise {
  constructor(executor) {
      this.onSuccess = null
      this.onFailed = null
      this.isFullfilled = false
      this.isRejected = false
      this.isCalled = false
      this.value
      executor(this.resolve.bind(this), this.reject.bind(this))
  }


  static resolve(value){
      return new MyPromise((res,rej)=>{
          res(value)
      })
  }
  static reject(value){
      return new MyPromise((res,rej)=>{
          rej(value)
      })
  }

  then(cb) {
      this.onSuccess = cb
      if (this.isFullfilled && !this.isCalled) {
          this.isCalled = true
          this.onSuccess(this.value)
      }
      return this
  }
  catch(cb) {
      this.onFailed = cb
      if (this.isRejected && !this.isCalled) {
          this.isCalled = true
          this.onFailed(this.value)
      }
      return this
  }


  resolve(successData){
      this.isFullfilled = true
      this.value = successData
      if (typeof this.onSuccess == "function") {
          this.onSuccess(successData)
          this.isCalled = true
      }


  }


  reject(errorMessage){
      this.isRejected = true
      this.value = errorMessage
      if (typeof this.onFailed == "function") {
          this.onFailed(errorMessage)
          this.isCalled = true
      }
  }


}


const myPromise = new MyPromise((res, rej) => {
  setTimeout(()=>{
   res("Good data")


  },1000)
})

myPromise.then((data) => {
  console.log(data)
}).catch((err) => {
  console.log("error", err)
})

```
---  

## 🚀Promise.all() 
### Promise.all() - It executes all passed promises concurrently and improves the performance of the application.

## 💡Promise.all() Cases :-
* #### 1) If all promises resolve, returns the array of results of all promises resolved.
* #### 2) If any promise fails, returns the rejected promise error.
* #### 3) If passed empty [], returns empty [].

https://www.youtube.com/watch?v=qOsqjVJ1p_k
Watch this video


## Example:-
```js
const t1 = () =>{
  return new Promise((resolve,reject)=>{
      setTimeout(()=>{
          resolve('t1 success');
      },500);
  })
}
const t2 = () =>{
  return new Promise((resolve,reject)=>{
      setTimeout(()=>{
          reject('t2 failed');
      },500);
  })
}
const t3 = () =>{
  return new Promise((resolve,reject)=>{
      setTimeout(()=>{
          resolve('t3 success');
      },500);
  })
}


Promise.all([t1(), t2(), t3()])
.then((res)=>{
  console.log(res);
}).catch(err=>{
  console.log(err);
})
```

## 📌Prototype Polyfills Promise.all() :-
```js
const t1 = () =>{
  return new Promise((resolve,reject)=>{
      setTimeout(()=>{
          resolve('t1 success');
      },500);
  })
}
const t2 = () =>{
  return new Promise((resolve,reject)=>{
      setTimeout(()=>{
          reject('t2 failed');
      },500);
  })
}
const t3 = () =>{
  return new Promise((resolve,reject)=>{
      setTimeout(()=>{
          resolve('t3 success');
      },500);
  })
}

Promise.myPromiseAll = function (promises) {
  return new Promise((resolve, reject) => {
      if (!Array.isArray(promises)) {
          reject(new Error('promises arguments must be an array'));
          return;
      }
      const result = [];
      let promiseCount = 0;
      const n = promises.length
      if (n === 0) {
          resolve(result);
          return;
      }
      promises.forEach(async (promiseFunc, index) => {
          try {
              const res = await promiseFunc;
              result[index] = res;
              promiseCount = promiseCount + 1;
              console.log(promiseCount);
              if (promiseCount === n)
                  resolve(result);
          } catch (err) {
              reject(err);
          }
      })
  })
}
Promise.myPromiseAll([t1(), t3()])
  .then(result => {
      console.log(result)
  }).catch(err => {
      console.log('Error: ', err);
  })
```
---  

## 🚀Promise.allSettled()
 ### Promise.allSettled() returns a promise that gets resolved when all passed promises are settled ( either fulfilled or rejected ) and in result it gives an array of objects having status and the value/reason of each promise.

* ####💡 Note :- If passed empty [], returns empty [].

https://www.youtube.com/watch?v=DbEzM_c4k8g
(watch this video)


```js
const t1 = () =>{
  return new Promise((resolve,reject)=>{
      setTimeout(()=>{
          // reject('t1 failed');
          resolve('t1 success');
      },500);
  })
}
const t2 = () =>{
  return new Promise((resolve,reject)=>{
      setTimeout(()=>{
          reject('t2 failed');
          // resolve('t2 success');
      },500);
  })
}
const t3 = () =>{
  return new Promise((resolve,reject)=>{
      setTimeout(()=>{
          // reject('t3 failed');
          resolve('t3 success');
      },500);
  });
}
Promise.allSettled([t1(), t2(), t3()])
.then((res)=>{
  console.log(res);
}).catch(err=>{
  console.log(err);
})
```

## Output:-
```js
[
  { status: 'fulfilled', value: 't1 success' },
  { status: 'rejected', reason: 't2 failed' },
  { status: 'fulfilled', value: 't3 success' }
]
```
## 📌Prototype Polyfills of Promise.allSettled() :-
```js
Promise.allSettledPolyfill = function(arr){
  console.log(arr);
  const result = arr.map((promise)=>{
      return Promise.resolve(promise).then((value)=>{
          return {
              status: 'fulfilled',
              value: value
          }
      }).catch((reason)=>{
          return {
              status: 'rejected',
              reason: reason
          }
      })
  });
  return Promise.all(result);
}


Promise.allSettledPolyfill([t1(),t2(),t3()])
  .then(res=>{
      console.log(res);
  })
```
---  

## 🚀Promise.any()
### Promise.any() - It executes all passed promises concurrently and returns the first resolved promise result.

##💡Promise.any() Cases :-
* #### 1) If no promise passes, returns the AggregateError "All promises were rejected".
* #### 2) If passed empty [], returns error.

https://www.youtube.com/watch?v=yEEW78qg-48
Watch this video

```js
const t1 = () =>{
  return new Promise((resolve,reject)=>{
      setTimeout(()=>{
          // reject('t1 failed');
          resolve('t1 success');
      },1500);
  })
}
const t2 = () =>{
  return new Promise((resolve,reject)=>{
      setTimeout(()=>{
          // reject('t2 failed');
          resolve('t2 success');
      },1000);
  })
}
const t3 = () =>{
  return new Promise((resolve,reject)=>{
      setTimeout(()=>{
          // reject('t3 failed');
          resolve('t3 success');
      },2500);
  });
}


Promise.any([t1(), t2(), t3()])
  .then((result)=>{
      console.log(result)
  }).catch((err)=>{
      console.log(err);
  })
```

### Output:-
```js
t2 success
```

## 📌Prototype Polyfills of Promise.any():-
```js
Promise.myAny = function(arr){
  return new Promise((resolve,reject)=>{
      let count = 0;
      arr.forEach((promise)=>{
          promise.then((result)=>{
              resolve(result);
          }).catch((err)=>{
              count++;
              if(count === arr.length){
                  reject(new Error('AggregateError: All promises were rejected'))
              }
          })
      })
  })
}
Promise.myAny([t1(), t2(), t3()])
  .then((result)=>{
      console.log(result)
  }).catch((err)=>{
      console.log(err);
  })
```
---  

 ## Promise.race() 
### It executes all passed promises concurrently and returns the first resolved or rejected promise result.

## 💡Promise.race() Case :-
* #### 1) If passed empty [], forever pending.
```js
const t1 = () =>{
  return new Promise((resolve,reject)=>{
      setTimeout(()=>{
          // reject('t1 failed');
          resolve('t1 success');
      },500);
  })
}
const t2 = () =>{
  return new Promise((resolve,reject)=>{
      setTimeout(()=>{
           reject('t2 failed');
        //   resolve('t2 success');
      },300);
  })
}
const t3 = () =>{
  return new Promise((resolve,reject)=>{
      setTimeout(()=>{
          // reject('t3 failed');
          resolve('t3 success');
      },1000);
  });
}


Promise.race([t1(), t2(), t3()])
    .then((result)=>{
        console.log(result)
    }).catch((err)=>{
        console.log('err ',err);
    })

```

## Output:-
```js
err  t2 failed
```

## 📌Prototype Polyfills of Promise.race() :-
```js
Promise.myRace = function(arr){
  return new Promise((resolve,reject)=>{
      arr.forEach((promise)=>{
          Promise.resolve(promise).then((result)=>{
              return resolve(result);
          }).catch((err)=>{
              return reject(err);
          })
      })
  })
}
Promise.myRace([t1(), t2(), t3()])
  .then((result)=>{
      console.log(result)
  }).catch((err)=>{
      console.log('err ',err);
  })
```
---  

## 🚀Debouncing:-
#### Debouncing is a technique used to improve the performance of applications by reducing the rate of functions call

#### 👉 If the function is getting called continuously, We can delay the function call for some time with the help of debouncing to optimize the performance of applications

## 💡use cases :-
* #### 👉 For mostly we used Search Box
* #### 👉 Continuous button click event function call can be delay.
* #### 👉 Resize of window event function call can be delay.

## 💡Let's take an example search input value-
https://www.youtube.com/watch?v=pkvXAM3uIZ8  (watch this video for better understanding)


#### In a search bar, you can use debouncing to delay sending an API request until the user has finished typing or paused for a moment. 
#### This prevents excessive requests for each keystroke.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Document</title>
  </head>

  <body>
    <h3>Debouncing Example</h3>
    <input type="text" id="search-input" placeholder="Search..." />
    <script src="debounce.js"></script>
  </body>
</html>
```

## debounce.js
```js
// Debounce function to delay the execution of the function
const debounce = (func, delay) => {
  let decouncing;
  return function () {
    const args = arguments;
    const ctx = this;
    clearTimeout(decouncing); // Clear the previous timeout
    decouncing = setTimeout(() => func.apply(ctx, args), delay); // Set the new timeout
  };
};

// Function to call the API (simulated)
const callAPI = function (term) {
  console.log("Calling API for", term);
};

// Create the debounced version of the API call
const debouncedAPI = debounce(callAPI, 500);

// Listen to input changes and trigger the debounced API call
document.getElementById("search-input").addEventListener("input", function (e) {
  debouncedAPI(e.target.value);
});

```
### 📝 Explanation:
`debounce(func, delay):`

* #### This function accepts a callback function (func) and a delay (in milliseconds).

* #### It ensures that func is only executed after the user stops performing the action (e.g., typing in the search bar) for delay milliseconds.

`callAPI(term):`

* #### This is a function that simulates calling an API based on the search term.

`Event Listener:`

* #### The input event is added to the search input field. As the user types, the debouncedAPI function is triggered, but due to debouncing, the actual callAPI function will only be called after the user stops typing for 500ms.

---  

## 🚀Throttling
### Throttling is a technique used to improve the performance of applications by limiting the rate of function calls
* #### 👉 If the function is getting called continuously, We can execute the function once in the given time interval with the help of Throttling to optimize the performance of applications
### 💡Debouncing vs Throttling-
* #### In Debouncing, the attached function will be executed only after the given time once the user stops calling the event.
* #### While in Throttling, the attached function will be executed only once in a given time interval.
* #### 💡Which technique to use in a particular scenario?
* #### For Search bar, It’s recommended to use Debouncing technique as it will give better user experience
* #### For Shooting game, Browser resizing and Scrolling feeds, It’s recommended to use Throttling technique.

```html
HTML 

<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Document</title>
  </head>


  <body>
    <h3>Throttling example</h3>
    <button id="myButton">shoot enemy</button>


    <script src="throttling.js"></script>
  </body>
</html>
```
## throttling.js
```js
// Throttling function to limit the frequency of a function call
const throttle = (func, limit) => {
    let isThrottling;
    return function () {
        const args = arguments;
        const ctx = this;
        if (!isThrottling) {
            func.apply(ctx, args);  // Execute the function
            isThrottling = true;
            setTimeout(() => isThrottling = false, limit);  // Reset after the time limit
        }
    };
};

// Function to simulate shooting (e.g., in a game)
function shoot() {
    console.log("Function called");
}

// Create a throttled version of the shoot function with a limit of 500ms
const throttledShoot = throttle(shoot, 500);

// Listen for button click event and trigger throttledShoot
document.getElementById("myButton").addEventListener("click", () => {
    throttledShoot();
});


```

## 📝 Explanation:
`throttle(func, limit):`

* #### This function accepts a callback function (func) and a limit (in milliseconds).

* #### It ensures that func is executed only once every limit milliseconds, even if the event is triggered multiple times during that interval.

`shoot():`

* #### This is a function that simulates shooting in a game or any other scenario that requires repeated actions.

`Event Listener:`

* #### The throttled version of the shoot() function is triggered every time the button is clicked, but due to throttling, it can only be executed once every 500ms.

---  

## 🚀Function currying
### It is a technique in functional programming that transforms the function of multiple arguments into several functions of a single argument in sequence. 

```js
function simpleFunction(param1, param2, param3) =>

function curriedFunction(param1)(param2)(param3)
```

#### We simply wrap a function inside a function, which means we are going to return a function from another function to obtain this kind of translation. The parent function takes the first provided argument and returns the function that takes the next argument and this keeps on repeating till the number of arguments ends. Hopefully, the function that receives the last argument returns the expected result.  


### Why is currying useful in javaScript ?

* It helps us to create a higher-order function
* It reduces the chances of error in our function by dividing it into multiple smaller functions that can handle one responsibility.
* It is very useful in building modular and reusable code
* It helps us to avoid passing the same variable multiple times
* It makes the code more readable

```js
function calculateVolume(length) {
	return function (breadth) {
		return function (height) {
			return length * breadth * height;
		}
	}
}
console.log(calculateVolume(4)(5)(6));
```




## Write a currying function that takes infinite arguments.
```js
const sum = function(a) {
    // Define an inner function that will take the next argument
    const innerSum = function(b) {
      // If there is a second argument (b), continue the recursion by calling sum with the accumulated value
      if (b) {
        return sum(a + b);
      }
      // If no second argument (b) is provided, return the accumulated sum (a)
      return a;
    };
 
    // Return the inner function so that more arguments can be provided
    return innerSum;
  };
 
  // Usage Examples
  console.log(sum(1)(2)(3)());       // 6
  console.log(sum(5)(10)(-3)(2)());  // 14
```




## Interview Question 1

### So how do we write a wrapper function curry which accepts a function say func and returns the curried version of func.

### Solution🚀

* Let's pass a function func as input.
* So to get the curried version of func, first thing we should do is return a function which takes arguments. In our case we are returning curried.
* Now in curried we need to check the length of arguments that are passed to it. If all the arguments are passed we call func else we need to again return a function to get the remaining arguments and so on until all the arguments are passed.
* So we can see a recursive behavior here. So how do we achieve this?
* We call curried recursively until all the arguments are received.

```js
function curry(func) {
    function curried(...args) {
        if(args.length >= func.length) {
            return func(...args);
        } else {
            return function(...more) {
                return curried(...args,...more);
            }
        }
    }
    return curried;
}

function multiply(a, b, c) {
    return a*b*c;
}

// To get the curried version of multiply we pass it to our above curry function.
let curried = curry(multiply);
console.log(curried(2)(3)(4)); // 24
console.log(curried(2,3)(4));  // 24
console.log(curried(2,3,4));  // 24
console.log(curried(5)(6,7)); // 210
```
---  

## 🚀Flatten an array

#### Means to convert an original array into a new array. It does this by collecting and concatenating the sub-arrays in an array into a single array.

#### We have two method in js to flatten the array
`Falt()`    and `flatmap()`
```js
const arr2 = [ [ [ 1,  2 ] , 3, 4, 5] ] ;
Console.log ( arr2.flat ( 2 ) );
// expected output 
[1, 2, 3, 4, 5]
```

* #### The flatMap() method uses a combination of the map() and flat() methods to perform operations.
* #### The flatMap() loops through the elements of an array and concatenates the elements into one level. flatMap() takes in a callback function which takes in the current element of the original array as a parameter.
```js
const arr3 = [1, 2, [ 4, 5 ], 6, 7, [ 8 ] ] ;
console.log(arr3.flatMap((element) => element)); 
// expected output 
[1, 2, 4, 5, 6, 7, 8]
```
## Key Takeaways:
* #### Use flat() when you need to flatten arrays of any depth.

* #### Use flatMap() when you want to map the array and flatten it in a single operation.

  ---
  

## 🚀Write custom function for Array.flat() using both recursive and iterative

## 📌Recursive Approach (No Depth)
```js
const flattenRecursive = (arr) => {
  if (!Array.isArray(arr)) {
    throw new Error("Input must be an array");
  }
  const result = [];
  for (const ele of arr) {
    if (Array.isArray(ele)) {
      result.push(...flattenRecursive(ele)); // Recursively flatten sub-arrays
    } else {
      result.push(ele); // Add non-array elements directly
    }
  }
  return result;
};

// Test case for Recursive Approach
const resultRecursive = flattenRecursive(
  [[[[0]], [1]], [[[2], [3]]], [[4], [5]]]
);
console.log(resultRecursive, "Recursive Result");
// Expected Output: [0, 1, 2, 3, 4, 5]
```
## 📌Iterative Approach (No Depth)
```js
const flattenIterative = (arr) => {
  if (!Array.isArray(arr)) {
    throw new Error("Input must be an array");
  }
  const stack = [...arr];
  const result = [];
  while (stack.length) {
    const ele = stack.pop();
    if (Array.isArray(ele)) {
      stack.push(...ele); // Push elements of the sub-array to the stack
    } else {
      result.push(ele); // Add non-array elements directly
    }
  }
  return result.reverse(); // Reverse the result to maintain order
};

// Test case for Iterative Approach
const resultIterative = flattenIterative([[[[0]], [1]], [[[2], [3]]], [[4], [5]]]);
console.log(resultIterative, "Iterative Result");
// Expected Output: [0, 1, 2, 3, 4, 5]
```
## 📌Recursive Approach with Depth

```js
const flattenRecursiveWithDepth = (arr, depth) => {
  if (!Array.isArray(arr)) {
    throw new TypeError("The first argument must be an array.");
  }
  let result = [];
  if (depth === 0) return arr; // Return the array as is when depth is 0
  for (let ele of arr) {
    if (Array.isArray(ele) && depth > 0) {
      result.push(...flattenRecursiveWithDepth(ele, depth - 1)); // Flatten sub-arrays up to the given depth
    } else {
      result.push(ele); // Add non-array elements directly
    }
  }
  return result;
};

// Test case for Recursive Approach with Depth
const result = flattenRecursiveWithDepth(
  [[[[[0]]], [1]], [[[2], [3]]], [[4], [5]]], 1
);
console.log(result);
// Expected Output: [ [ [ 0 ] ], 1, [ [ 2 ], [ 3 ] ], 4, 5 ]
```
## 📌Iterative Approach with Depth
```js
const flattenIterativeWithDepth = (arr, depth) => {
  if (!Array.isArray(arr)) {
    throw new TypeError("The first argument must be an array.");
  }
  let result = [];
  let stack = [...arr]; // Start with the original array
  let currentDepth = 0;

  // Iterate while there are elements in the stack and we haven't reached the max depth
  while (stack.length) {
    const ele = stack.pop();

    // If depth is greater than 0 and the element is an array, we need to flatten further
    if (Array.isArray(ele) && currentDepth < depth) {
      stack.push(...ele); // Push the elements of the array onto the stack
      currentDepth++; // Increment the depth level
    } else {
      result.push(ele); // Add non-array elements or if we've reached the depth to the result
    }
  }

  return result.reverse(); // Reverse to maintain original order
};

// Test case for Iterative Approach with Depth
const resultIterativeWithDepth = flattenIterativeWithDepth(
  [[[[[0]]], [1]], [[[2], [3]]], [[4], [5]]], 1
);
console.log(resultIterativeWithDepth);
// Expected Output: [ [ [ 0 ] ], 1, [ [ 2 ], [ 3 ] ], 4, 5 ]
```







