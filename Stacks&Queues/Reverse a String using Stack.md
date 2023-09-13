# Reverse a String using Stack

This JavaScript function reverses a string using a stack data structure. It has a time complexity of O(N) and a space complexity of O(N).

```javascript
const reversedString = (string) => {
    var stack = [];
    var reversedString = '';

    for (let i = 0; i < string.length; i++) {
        stack.push(string[i]);
    }

    while (stack.length > 0) {
        reversedString += stack.pop();
    }

    return reversedString;
}

console.log(reversedString("hello"));
