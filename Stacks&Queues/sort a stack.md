# Sort a Stack using Nested Loops

This JavaScript code demonstrates how to sort a stack using nested loops. The time complexity of the `sortStack` function is O(n^2), where n is the number of elements in the stack. The space complexity is O(n) due to the space used by the two stacks: `stack` and `sortedStack`.

```javascript
// Sort a Stack using Nested Loops
// Time Complexity (TC):
//   The function uses a nested while loop to move elements between the original stack and the sortedStack.
//   In the worst case scenario, each element from the original stack is moved to the sortedStack once.
//   Therefore, the time complexity of the sortStack function is O(n^2), where n is the number of elements in the stack.
// Space Complexity (SC):
//   The space complexity of the sortStack function depends on the space used by the two stacks: stack and sortedStack.
//   In the worst case, both stacks may contain all n elements from the original stack.
//   Therefore, the space complexity of the sortStack function is O(n) due to the two stacks.

function sortStack(stack) {
    const sortedStack = [];

    while (stack.length > 0) {
        const temp = stack.pop();

        while (sortedStack.length > 0 && sortedStack[sortedStack.length - 1] > temp) {
            stack.push(sortedStack.pop());
        }

        sortedStack.push(temp);
    }

    // Now, the sortedStack contains the sorted elements.
    return sortedStack;
}

// Example usage:
const stack = [34, 3, 31, 98, 92, 23];
console.log("Original stack: " + stack);

const sortedStack = sortStack(stack);

console.log("Sorted stack: " + sortedStack);
```

# OR

# Sort a Stack using Recursion

This JavaScript code demonstrates how to sort a stack using a recursive approach. The time complexity of the `sortStack` function is approximately O(n^2), where n is the number of elements in the stack. The space complexity is O(n) due to the space used for the call stack and the auxiliary stack.

```javascript
// Sort a Stack using Recursion
// Time Complexity (TC):
//   In the worst case, the sortStack function has to recursively call itself for every element in the stack.
//   In each recursive call, it moves elements from the main stack to the auxiliary stack until it finds the correct position for the popped element x.
//   The maximum number of recursive calls is equal to the number of elements in the stack.
//   For each element, there are potentially multiple iterations in the while loop to find the correct position.
//   Therefore, the time complexity of this sorting algorithm is approximately O(n^2), where n is the number of elements in the stack.
// Space Complexity (SC):
//   The space complexity is determined by the space used for the call stack due to recursion and the additional space used for the tempStack auxiliary stack.
//   In the worst case, when the stack is completely reversed, the maximum depth of the call stack will be equal to the number of elements in the stack.
//   Additionally, the tempStack can also hold all the elements in the stack in the worst case.
//   Therefore, the space complexity of this algorithm is O(n) due to the call stack and the auxiliary stack.

function sortStack(s) {
    // If the stack is empty or has only one element, return
    if (s.length <= 1) {
        return;
    }

    // Remove the top element of the stack
    let x = s.pop();

    // Sort the remaining elements in the stack using recursion
    sortStack(s);

    // Create two auxiliary stacks
    let tempStack = [];

    // Move all elements that are greater than x from the main stack to the tempStack
    while (s.length !== 0 && s[s.length - 1] > x) {
        tempStack.push(s.pop());
    }

    // Push x back into the main stack
    s.push(x);

    // Move all elements from tempStack back to the main stack
    while (tempStack.length !== 0) {
        s.push(tempStack.pop());
    }
}

// Create a stack
let s = [];

// Push elements into the stack
s.push(34);
s.push(3);
s.push(31);
s.push(98);
s.push(92);
s.push(23);

// Sort the stack
sortStack(s);

// Print the sorted elements
let result = "Sorted numbers are: ";
while (s.length !== 0) {
    result += s.pop() + " ";
}
console.log(result.trim());
