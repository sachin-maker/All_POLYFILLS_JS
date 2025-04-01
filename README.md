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


## Map()  =>

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


## filter()  =>
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

## Reduce ()=>
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

## Find() =>

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

## findIndex() =>
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
## forEach() =>
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


