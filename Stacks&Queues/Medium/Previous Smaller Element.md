# Find prev smaller element
# TC - O(N)
# SC - O(N)

```js 
const nextSmallestElement = (A) => {
    var stack = [];
        stack.push(-1);
        var ans = [];

        for(let i = 0; i < A.length - 1; i++){
            var curr = A[i];
            while(stack[stack.length - 1] > curr && stack[stack.length - 1]!==-1 ){
                stack.pop();
            }
            ans[i] = stack[stack.length - 1];
            stack.push(curr);
        }
        return ans;
}

console.log(nextSmallestElement([1, 3, 5, 3, 7, 8]));