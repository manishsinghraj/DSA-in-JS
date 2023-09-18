## Find Next Smaller Element

### Time Complexity: O(N)
### Space Complexity: O(N)

```javascript
const nextSmallestElement = (n1) => {
    const stack = [];
    const ans = new Array(n1.length).fill(-1);

    stack.push(-1);

    for (let i = n1.length - 1; i >= 0; i--) {
        const curr = n1[i];
        while (stack[stack.length - 1] > curr) {
            stack.pop();
        }
        ans[i] = stack[stack.length - 1];
        stack.push(curr);
    }

    return ans;
}

console.log(nextSmallestElement([1, 3, 5, 3, 7, 8]));
