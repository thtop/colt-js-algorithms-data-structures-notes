## Intro to Big O

### Objectives
- Motivate the need for something like Big O Notation 
- Describe what Big O Notation is
- Simplify Big O Expressions
- Define "time complexity" and "space complexity"
- Evaluate the time complexity and space complexity if different algorithms using Big O Notation
- Describe what a logarithm is

### What's the idea here?

- Imageine we have multiple implementations of the same function.
- How can we determine which one is the "bast?"
- Write a function that accepts a string input and returns a reversed copy


- Great!
- Pretty Good
- Only OK
- Ehhhhhhhhh
- Awful

### Who Cares?

- It's important to have a precise vocabulary to talk about how our code preforms
- Useful for discussing trade-offs between different approaches 
- When you code slows down or crashes, identifying parts of the code that are inefficient can help us find pain points in our applications
- Less important: it comes up in interviews!

### An Example 

- Suppose we want to write a function that calculates the sum of all numbers from 1 up to (and including) some number *n*.

1)
```js
function addUpTo(n) {
  let total = 0;
  for (let i = 1; i <= n; i++) {
    total += i;
  }
  return total;
}

console.log(addUpTo(6));

```

2)
```js
function addUpTo(n) {
  return n * (n + 1) / 2;
}

console.log(addUpTo(6));

```

### What does better mean?

- Faster?
- Less memory-intersive?
- More readable?

### Why not use timers?

1)
```js
function addUpTo(n) {
  let total = 0;
  for (let i = 1; i <= n; i++) {
    total += i;
  }
  return total;
}

let t1 = performance.now();
addUpTo(1000000000);
let t2 = performance.now();
console.log(`Time Elapsed: ${(t2 - t1) / 1000} seconds.`);

// Time Elapsed: 1.0208450000500306 seconds.

```

2)
```js
function addUpTo(n) {
  return n * (n + 1) / 2;
}

let t1 = performance.now();
addUpTo(1000000000);
let t2 = performance.now();
console.log(`Time Elapsed: ${(t2 - t1) / 1000} seconds.`);

// Time Elapsed: 0.000020000035874545574 seconds.

```

### The Problem with Time

- Different machines will record different times
- The same machine will record different times!
- For fast algorithms, speed measurements may not be precise enough?