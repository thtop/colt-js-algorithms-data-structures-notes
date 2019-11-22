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

### If not time, then what?

- Rather than counting seconds, which are so variable...
- Let's count the number of simple operations the computer has t perform!

- Counting Operations

```js
function addUpTo(n) {
  return n * (n + 1) / 2;
}
```
1 multiplicaton
1 addition
1 division
- 3 simple operations, regardles of the size of *n*

---

```js
function addUpTo(n) {
  let total = 0;
  for (let i = 1; i <= n; i++) {
    total += i;
  }
  return total;
}
```

- *n* additions
- *n* assignments
- *n* additins and
- *n* addignments
- 1 assignment
- 1 assingment
- n comparisons

### Counting is hard!

- Depending on what we count, the number of operations can be as low as 2n or high as 5n + 2
- But regardless of the exact number, the number of operations grows roughly *propritonally with n*

### Introducing ... Big O
 - Big O Notation is a way to formalize fuzzy counting
 - It allows us to talk formally about how the runtime of an algorithm grows as the inputs grow 
 - We won't care about the details, only the trends


### Big O Definition

- We say that an algorithm is **O(f(n))** if the number of simple operations the computer has to do is eventually less than a constant times **f(n)**, as **n** increases

- f(n) could be linear (f(n) = n)
- f(n) could be quadratic (f(n) = n2)
- f(n) could be constant (f(n) = 1)
- f(n) could be something entirely different!

### Example

```js
function addUpTo(n) {
  return n * (n + 1) / 2;
}
```
- Always 3 operations **O(1)**


```js
function addUpTo(n) {
  let total = 0;
  for (let i = 1; i <= n; i++) {
    total += i;
  }
  return total;
}
```

- Number of operations is (eventually) bounded by a multiple of n (say, 10n) => **O(n)**
--- 

### Another Example

```js
function countUpAndDown(n) {
  console.log("Ging up!");
  for (let i = 0; i < n; i++) {
    console.log(i);
  } // O(n)
  
  console.log("At the top!\nGoing down...");
  for (let j = n - 1; j >= 0; j--) {
    console.log(j);
  } // O(n)

  console.log("Back down. Bye!")
}

countUpAndDown(10);

```

### OMG More Examplez

```js
function printAllPairs(n) {
  for(var i = 0; i < n; i++) {
    for (var j = 0; j < n; j++) {
      console.log(i, j)
    }
  }
}


printAllPairs(5); // O(n2)
```

### Simplifying Big O Expressions

- when determining the time complexity of an algorithm, there are some helpful rule of thumbs for big O expressions.

**Constants Dont't Matter**
- O(2n)    ->  O(n)
- O(500)   ->  O(1)
- O(13n^2) ->  O(n^2)

**Smaller Terms Don't Matter**

- O(n + 10)        -> O(n)
- O(1000n + 50)    -> O(n)
- O(n^2 + 5n + 8)  -> O(n^2)

### Big O Shorthands

- Analyzing complexity with big O can get complicated
- There are several rules of thumb that can help 
- These rules won't **ALWAYS** work, but are a helpful starting point

1. Arithmetic operations are constant
2. Variable assignment is constant
3. Accessing elements in an array (by index) or object (by key) is constant
4. In a loop, the the complexity is the lenght of the loop times the complexity of whatever happens inside of the loop