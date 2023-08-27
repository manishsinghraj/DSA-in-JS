## Sort an Array of 0s, 1s, and 2s

### Problem Statement
Given an array consisting of only 0s, 1s, and 2s, write a program to in-place sort the array without using inbuilt sort functions. (Expected: Single pass-O(N) and constant space)

### Examples
- **Input:** nums = [2,0,2,1,1,0]
  **Output:** [0,0,1,1,2,2]
  
- **Input:** nums = [2,0,1]
  **Output:** [0,1,2]
  
- **Input:** nums = [0]
  **Output:** [0]

#### Brute Approach
**Time Complexity:** O(N * logN)
**Space Complexity:** O(1)
*Note:* This approach uses sorting functions like merge or quick sort.

#### Better Approach
**Time Complexity:** O(N) + O(N), where N is the size of the array. First O(N) for counting the number of 0’s, 1’s, 2’s, and second O(N) for placing them correctly in the original array.
**Space Complexity:** O(1) as we are not using any extra space.

```javascript
const sortGivenNumbers = (a, n) => {
    var cnt0 = 0, cnt1 = 0, cnt2 = 0;

    for (let i = 0; i < n; i++) {
        if (a[i] == 0) cnt0++;
        else if (a[i] == 1) cnt1++;
        else cnt2++;
    }

    for (let i = 0; i < cnt0; i++) {
        a[i] = 0;
    }
    for (let i = cnt0; i < cnt0 + cnt1; i++) {
        a[i] = 1;
    }
    for (let i = cnt0 + cnt1; i < n; i++) {
        a[i] = 2;
    }
    return a;
}

let arr = [0, 1, 1, 2, 2, 0, 0];
var n = arr.length;

console.log(sortGivenNumbers(arr, n));
```