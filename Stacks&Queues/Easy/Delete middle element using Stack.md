# Delete Middle Element using Stack

This JavaScript function deletes the middle element from a stack. It takes two parameters: the original stack and the middle element to be deleted.

```javascript
const deleteMiddleEle = (stacks, x) => {
    var stack = [...stacks];
    var temp = [];
    var count = 0;
    const middle = Math.floor(stack.length / 2);

    while (stack.length > 0) {
        if (middle !== count) {
            const popped = stack.pop();
            temp.push(popped);
        } else {
            stack.pop();
        }
        count++;
    }

    return temp.reverse();
}

console.log(deleteMiddleEle([1, 2, 4, 5, 7, 8]));
