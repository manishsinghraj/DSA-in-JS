## Redundant Brackets

### Time Complexity: O(N^2)
### Auxiliary Space: O(N) (use of Stack)

```javascript
function hasRedundantBrackets(expression) {
    const stack = [];

    for (const char of expression) {
        if (char === '(' || char === '+' || char === '-' || char === '*' || char === '/') {
            stack.push(char);
        } else if (char === ')') {
            let top = stack[stack.length - 1];
            if (top === '(') {
                return true;
            } else {
                while (top !== '(') {
                    stack.pop();
                    top = stack[stack.length - 1];
                }
                stack.pop(); // Remove the open bracket '('
            }
        }
    }

    return false; // No redundant brackets found
}

const expression1 = "(a + b)";
console.log(hasRedundantBrackets(expression1)); // Output: false

const expression2 = "((a + b) * (c - d))";
console.log(hasRedundantBrackets(expression2)); // Output: false

const expression3 = "(a + b) * (c - d)";
console.log(hasRedundantBrackets(expression3)); // Output: false

const expression4 = "(a + b) * ((c - d))";
console.log(hasRedundantBrackets(expression4)); // Output: true

const expression5 = "(a)";
console.log(hasRedundantBrackets(expression5)); // Output: true

const expression6 = "((a/b))";
console.log(hasRedundantBrackets(expression6)); // Output: true
```