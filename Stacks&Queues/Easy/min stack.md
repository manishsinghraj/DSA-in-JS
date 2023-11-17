# Min Stack Implementation

## Problem Statement
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

## Example

```javascript
// Input Format
["MinStack", "push", "push", "push", "getMin", "pop", "top", "getMin"]
[
    [], [-2], [0], [-3], [], [], [], []
]

// Result
[null, null, null, null, -3, null, 0, -2]


// ## Explanation
// This code implements a `MinStack` class that allows you to push elements onto the stack, pop elements from the stack, get the top element, and get the minimum element in the stack efficiently.

// Define the MinStack class
var MinStack = function () {
    this.stack = [];     // Main stack to store elements
    this.minStack = [];  // Auxiliary stack to keep track of the minimum element
};

// ### `push(val)`
// - **Time Complexity (TC):** O(1)
// - **Space Complexity (SC):** O(1)
// This function pushes an element onto the stack and updates the `minStack` to keep track of the minimum element.
MinStack.prototype.push = function (val) {
    this.stack.push(val);
    if (this.minStack.length === 0 || val <= this.minStack[this.minStack.length - 1]) {
        this.minStack.push(val);
    }
};

// ### `pop()`
// - **Time Complexity (TC):** O(1)
// - **Space Complexity (SC):** O(1)
// This function pops the top element from the stack and updates the `minStack` if the popped element was the minimum.
MinStack.prototype.pop = function () {
    if (this.stack.length === 0) return;

    const poppedElement = this.stack.pop();

    if (poppedElement === this.minStack[this.minStack.length - 1]) {
        this.minStack.pop();
    }
};

// ### `top()`
// - **Time Complexity (TC):** O(1)
// - **Space Complexity (SC):** O(1)
// This function returns the top element of the stack.
MinStack.prototype.top = function () {
    if (this.stack.length === 0) return undefined; // Changed return; to return undefined;
    return this.stack[this.stack.length - 1]; // Corrected the return value
};

// ### `getMin()`
// - **Time Complexity (TC):** O(1)
// - **Space Complexity (SC):** O(n)
// The corrected space complexity for getMin() is O(n) because it uses an additional stack(minStack) to keep track of the minimum element at each step, and the space used in minStack grows linearly with the number of elements pushed onto the main stack.
MinStack.prototype.getMin = function () {
    if (this.stack.length === 0) return undefined; // Changed return; to return undefined;
    return this.minStack[this.minStack.length - 1];
};
```

# using both o(1)
```js
var MinStack = function () {
    this.stack = [];
};

MinStack.prototype.push = function (val) {
    let min = this.stack.length === 0 ? val : Math.min(val, this.getMin());
    this.stack.push({ val, min });
};

MinStack.prototype.pop = function () {
    if (this.stack.length === 0) return;
    this.stack.pop();
};

MinStack.prototype.top = function () {
    if (this.stack.length === 0) return undefined;
    return this.stack[this.stack.length - 1].val;
};

MinStack.prototype.getMin = function () {
    if (this.stack.length === 0) return undefined;
    return this.stack[this.stack.length - 1].min;
};

