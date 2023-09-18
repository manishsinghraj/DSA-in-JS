# Insert at Bottom of the Stack

This JavaScript function inserts an element at the bottom of a stack using an extra stack. It has a time complexity of O(N) and a space complexity of O(N).

## Using Extra Stack Space (Normal Code)

// TC: O(N)
// SC: O(N)
```javascript
const addElementAtBottom = (stacks, x) => {
    var stack = [...stacks];
    var temp = [];

    while (stack.length > 0) {
        temp.push(stack.pop());
    }

    stack.push(x);

    while (temp.length > 0) {
        stack.push(temp.pop());
    }

    return stack;
}

console.log(addElementAtBottom([1], 8));
```


# Insert at Bottom of the Stack using Recursion

This JavaScript function inserts an element at the bottom of a stack using recursion. It has a time complexity of O(n) and a space complexity of O(n) in the worst case.

```javascript
// Insert at Bottom of the Stack using Recursion
// Time Complexity (TC):
//   In the worst case, when the function is called with a non-empty stack of size n, it will make n recursive calls, each involving popping and pushing elements onto the stack.
//   Therefore, the time complexity of the function is O(n).
// Space Complexity (SC):
//   The space complexity is determined by the function's call stack due to recursion and the additional space required for the temporary variables.
//   In the worst case, the function will make n recursive calls, so the maximum depth of the call stack will be n.
//   Additionally, it uses two arrays, stack and temp, which can each store up to n elements in the worst case.
//   Therefore, the space complexity of the function is O(n) for both the call stack and the temporary arrays.
//   So, the time complexity is O(n), and the space complexity is O(n) in the worst case.

const addElementAtBottomRecursive = (stack, x) => {
    if (stack.length === 0) {
        stack.push(x); // Base case: If the stack is empty, just push the element.
    } else {
        const top = stack.pop(); // Remove the top element.
        addElementAtBottomRecursive(stack, x); // Recursively add the element to the bottom.
        stack.push(top); // Put the top element back on top.
    }
    return stack;
};

console.log(addElementAtBottomRecursive([], 8)); // Example with an empty stack
console.log(addElementAtBottomRecursive([1, 2, 3, 4, 5, 6], 8)); // Example with a non-empty stack
