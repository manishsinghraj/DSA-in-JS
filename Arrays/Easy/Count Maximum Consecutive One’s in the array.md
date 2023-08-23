## Count Maximum Consecutive One's in the Array

**Problem Statement:** Given an array that contains only 1 and 0, return the count of maximum consecutive ones in the array.

**Example 1:**

Input: `prices = [1, 1, 0, 1, 1, 1]`
Output: 3
Explanation: There are two consecutive 1's and three consecutive 1's in the array, out of which the maximum is 3.

Input: `prices = [1, 0, 1, 1, 0, 1]`
Output: 2
Explanation: There are two consecutive 1's in the array.

- **Time Complexity:** O(N), where N is the size of the array.
  - The solution involves a single pass through the array to calculate the count of consecutive ones.

- **Space Complexity:** O(1)
  - The algorithm uses a constant amount of extra space for variables.

```javascript
const MaxConsecutiveOnes = (a, n) => {
    var count = 0;
    var max = 0;
    for (let i = 0; i < n; i++) {
        if (a[i] == 1) {
            count++;
            if (count > max) {
                max = count;
            }
        }
        else count = 0;
    }

    return max;
}

let arr = [0, 1, 0, 1, 0, 0, 1];
console.log(MaxConsecutiveOnes(arr, arr.length));