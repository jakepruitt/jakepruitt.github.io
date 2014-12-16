---
layout: post
title: Functional
image: /images/functional.jpg
description: A walkthrough of the different functional methods of Arrays in JavaScript, and when to use each one.
---

![](/images/functional.jpg)

The ECMAScript 5 standard introduced a number of functional methods to the JavaScript `Array` type that you can now use in all modern browsers. Each method takes an anonymous callback function that is called on each element of the array. [Douglas Crockford](https://en.wikipedia.org/wiki/Douglas_Crockford), author of *JavaScript: The Good Parts* said that with the new functional methods, he does not use `for` loops any more. These functional methods allow you to perform complex array manipulation in very elegant and fluid ways, much cleaner than declaring a global iterating variable.

## The `for` loop - a baseline

The `for` loop is a basic construct in almost every programming language. Using simple logic, a `for` loop performs a certain block repeatedly until a counter variable reaches a limit. When iterating over an array, it is common to see the following pattern used for `for` loops:

```JavaScript
var arr = [0,1,1,2,3,5],
		total = 0;

for(var i = 0; i < arr.length; i++) {
	total += arr[i];
}

return total;
// >> 12
```

This loop begins with `i = 0` and iterates through the entire array, adding the element in the array at the i'th address to the total. It is not a total crime to `for` loops; they are seen in the wild quite a bit. The main deterrent from using `for` loops is that they block the script from continuing to run, thus hogging up precious time that may prevent the user from interacting with the page or increase load time of pages.

Our first functional method is very similar to a `for` loop.

## The `forEach` method - one step above

When using the `forEach` method, you should pass a function that is passed the element, the index of the element, and the entire array. The syntax looks a lot like a `for` loop:

```JavaScript
var arr = [0,1,1,2,3,5],
		total = 0;

arr.forEach(function(x,i,arr) {
	total += x;
});

return total;
// >> 12
```

We were able to clean up the code a little bit, but the `forEach` function basically performs the same function as a `for` loop. It is a block of code that performs an action on an element of an array. The subtle improvement here is that we could address the element by using the variable `x` rather than addressing the element using the index as in the `for` loop (`arr[i]`). We can add a lot of functionality to an iteration if we have it return a value.

## The `reduce` method - when all you want is one summary

The `reduce` method allows you to take an array and an initial value, and then perform actions on that initial value based on every array element until you have finished the array. The total example we have been using so far is a really great use case for `reduce`, in which we are adding each element to a total and returning the total. This can be reduced to the following code:

```JavaScript
var arr = [0,1,1,2,3,5];

var total = arr.reduce(function(sum, x, i, arr) {
	return sum + x;
}, 0);

return total;
// >> 12
```

This is a very terse way of writing the code, and can be reduced even more, down to 3 short lines:

```JavaScript
return [0,1,1,2,3,5].reduce(function(sum,x) {
	return sum + x;
});
// >> 12
```

Each time the function is called, the return statement is fed into the first argument of the next function call. The second argument of the `reduce` method is the initial value of the sum, which is zero by default. The `reduce` method returns the final output of the last function call.

## Map - when you want to transform an array

The `map` method of arrays lies at the heart of many functional programming paradigms, including immutable data structures. The idea of a map method is to take every element of an array and return a new array that has had the same operation performed on it. For instance, to double every element of an array, you could use the `map` method:

```JavaScript
var arr = [0,1,1,2,3,5];

var double = arr.map(function(x,i,arr) {
	return x * 2;
});

return double;
// >> [0,2,2,5,6,10]
```

This removes the need of creating a new array and pushing new elements in every iteration of a `for` loop. The fact that the `map` method returns an array can be very handy for composing `map` calls with other array methods, like finding the sum of the squares of an array:

```JavaScript
return [0,1,1,2,3,5].map(function(x) {
	return Math.pow(x,2);
}).reduce(function(sum,x) {
	return sum + x;
});
// >> 40
```

## Filter - slimming down your array

The `filter` method is used to create a new array with only certain elements of your input array. This is typically done with an `for` statement that checks a boolean expression with an `if` statement and pushes to an output array if it satisfies that condition. With the `filter` method the only thing you need to do is write an anonymous function that returns a boolean based on each element of the array. The filter method will then return the filtered array. For instance, if we want to filter the input function down to elements less than two, all we would need would be:

```JavaScript
return [0,1,1,2,3,5].filter(function(x) {
	return x < 2;
});
// >> [0,1,1]
```

All of these functional methods are very powerful, and there are some other methods that I did not cover, such as `some` and `every`, but I will save those for a "Secret JavaScript Tips" article, because those two have some very nice features.

Let me know if you have any more questions about functional methods!