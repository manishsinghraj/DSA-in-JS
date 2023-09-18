## Find Next Greater Element (Brute Force)

### Time Complexity: O(N^2)
### Space Complexity: O(N)

```javascript
var nextGreaterElement = function(nums1, nums2) {
    const ans = [];
    for(let i = 0; i < nums1.length; i++){
        let max = -1;
        for(let j = 0; j < nums2.length; j++){
            let index = j;
            if(nums1[i] === nums2[j]){
                while(index !== nums2.length){
                    if(nums2[index] > nums1[i]){
                        max = nums2[index];
                        break;
                    }
                    index++;
                }
            }
        }
        ans.push(max);
    }
    return ans;
};

```

## Find Next Greater Element

### Time Complexity: O(N)
### Space Complexity: O(N)

```javascript
const nextGreaterElement = (n1) => {
    const stack = [];
    const ans = new Array(n1.length).fill(-1);

    stack.push(-1);

    for (let i = n1.length - 1; i >= 0; i--) {
        const curr = n1[i];
        while (stack[stack.length - 1] <= curr && stack[stack.length - 1] !== -1) {
            stack.pop();
        }
        ans[i] = stack[stack.length - 1];
        stack.push(curr);
    }

    return ans;
}

console.log(nextGreaterElement([1, 3, 5, 3, 7, 8]));
```
