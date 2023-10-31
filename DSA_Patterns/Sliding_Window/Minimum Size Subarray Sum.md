## Minimum Size Subarray Sum

Given an array of positive integers `nums` and a positive integer `target`, return the minimal length of a subarray whose sum is greater than or equal to `target`. If there is no such subarray, return 0 instead.

### Example 1:

- Input: target = 7, nums = [2,3,1,2,4,3]
- Output: 2
- Explanation: The subarray [4,3] has the minimal length under the problem constraint.

- Input: target = 4, nums = [1,4,4]
- Output: 1

- Input: target = 11, nums = [1,1,1,1,1,1,1,1]
- Output: 0

- Constraints:
- 1 <= target <= 10^9
- 1 <= nums.length <= 10^5
- 1 <= nums[i] <= 10^4
- Follow up: If you have figured out the O(n) solution, try coding another solution of which the time complexity is O(n log(n)).

// bruteForce
// o(n^2)
```js
function minSubarraySum(arr, target) {
  let minLength = Infinity;

  for (let i = 0; i < arr.length; i++) {
    let currentSum = 0;

    for (let j = i; j < arr.length; j++) {
      currentSum += arr[j];

      if (currentSum >= target) {
        minLength = Math.min(minLength, j - i + 1);
        break;  // No need to check longer subarrays for this i
      }
    }
  }

  return minLength === Infinity ? 0 : minLength;
}

// Example usage:
const arr = [2, 3, 1, 2, 4, 3];
const target = 7;
console.log(minSubarraySum(arr, target)); // Output: 2 (Minimum subarray is [4, 3])
```

//Optimised
// o(n)
```js
function minSubarraySum(arr, target) {
  let minLength = Infinity;
  let left = 0;
  let currentSum = 0;

  for (let right = 0; right < arr.length; right++) {
    currentSum += arr[right];

    while (currentSum >= target) {
      minLength = Math.min(minLength, right - left + 1);
      currentSum -= arr[left];
      left++;
    }
  }

  return minLength === Infinity ? 0 : minLength;
}

// Example usage:
const arr = [2, 3, 1, 2, 4, 3];
const target = 7;
console.log(minSubarraySum(arr, target)); // Output: 2 (Minimum subarray is [4, 3])
```
