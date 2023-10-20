Smallest Subarray with a given sum
- const arr = [2, 3, 1, 2, 4, 3];
- const target = 7;

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
