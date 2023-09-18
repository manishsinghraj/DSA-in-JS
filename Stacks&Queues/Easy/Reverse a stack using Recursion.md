# Reverse a Stack using Recursion

This JavaScript code demonstrates how to reverse a stack using recursion. It has a time complexity of O(n) and a space complexity of O(n), where n is the number of elements in the stack.

```javascript
// Reverse a Stack using Recursion
// Time Complexity (TC):
//   The reverseStack function recursively calls itself until the stack is empty, popping and pushing elements in the process.
//   For each element in the stack, there is a constant amount of work (pushing and popping), and this work is done for each element in the stack.
//   Therefore, the time complexity of the reverseStack function is O(n), where n is the number of elements in the stack.
// Space Complexity (SC):
//   The space complexity is determined by the function's call stack due to recursion.
//   In the worst case, where the stack is completely reversed, the maximum depth of the call stack will be equal to the number of elements in the stack.
//   Therefore, the space complexity of the reverseStack function is O(n) due to the recursion stack.
//   The insertAtBottom function, which is called recursively by reverseStack, also contributes to the space complexity, but its space usage is dwarfed by the space used for the call stack. So, the dominant factor in space complexity is the recursion stack.

function reverseStack(stack) {
    if (stack.length === 0) {
        return;
    }

    var top = stack.pop();

    reverseStack(stack);

    insertAtBottom(stack, top);

    return stack;
}

function insertAtBottom(stack, topElement) {
    if (stack.length === 0) {
        stack.push(topElement);
        return;
    }

    const top = stack.pop(); // Remove the top element.
    insertAtBottom(stack, topElement); // Recursively add the element to the bottom.
    stack.push(top); // Put the top element back on top.
}

// Example usage:
const originalStack = [1, 2, 3, 4, 5];
const reversedStack = reverseStack(originalStack);

console.log(reversedStack); // Output: [5, 4, 3, 2, 1]
