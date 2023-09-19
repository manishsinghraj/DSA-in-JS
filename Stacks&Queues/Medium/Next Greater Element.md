## Find Next Greater Element 

## 496. Next Greater Element I
(Brute Force)
### Time Complexity: O(N^2)
### Space Complexity: O(N)
Example 1:

Input: nums1 = [4,1,2], nums2 = [1,3,4,2]
Output: [-1,3,-1]
Explanation: The next greater element for each value of nums1 is as follows:
- 4 is underlined in nums2 = [1,3,4,2]. There is no next greater element, so the answer is -1.
- 1 is underlined in nums2 = [1,3,4,2]. The next greater element is 3.
- 2 is underlined in nums2 = [1,3,4,2]. There is no next greater element, so the answer is -1.
Example 2:

Input: nums1 = [2,4], nums2 = [1,2,3,4]
Output: [3,-1]
Explanation: The next greater element for each value of nums1 is as follows:
- 2 is underlined in nums2 = [1,2,3,4]. The next greater element is 3.
- 4 is underlined in nums2 = [1,2,3,4]. There is no next greater element, so the answer is -1.
  
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


//TO DO
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
