Max Sum Subarray of size K

Input:
- N = 4, K = 2
- Arr = [100, 200, 300, 400]
- Output:
- 700
- Explanation:
- Arr3  + Arr4 =700,
- which is maximum.

```js
function slidingWindowBruteForce(arr, windowSize) {
  if (windowSize > arr.length) {
    return null; // Window size is larger than the array length
  }

  let maxSum = -Infinity; // Initialize maxSum with a very small value

  for (let i = 0; i <= arr.length - windowSize; i++) {
    let windowSum = 0;

    // Calculate the sum of elements in the current window
    for (let j = i; j < i + windowSize; j++) {
      windowSum += arr[j];
    }

    // Update maxSum if the current window's sum is greater
    if (windowSum > maxSum) {
      maxSum = windowSum;
    }
  }

  return maxSum;
}

// Example usage:
const array = [2, 4, 6, 8, 1, 3, 5, 7, 9];
const windowSize = 3;

const maxSum = slidingWindowBruteForce(array, windowSize);
console.log(`Maximum sum of ${windowSize}-size window: ${maxSum}`);
```

Better (Queue)
```js
function maxSumSubarray(arr, windowSize) {
  if (windowSize > arr.length) {
    return null; // Window size is larger than the array length
  }

  let maxSum = 0;
  let currentSum = 0;
  const windowQueue = [];

  for (let i = 0; i < arr.length; i++) {
    windowQueue.push(arr[i]);
    currentSum += arr[i];

    if (windowQueue.length > windowSize) {
      currentSum -= windowQueue.shift();
    }

    if (windowQueue.length === windowSize) {
      maxSum = Math.max(maxSum, currentSum);
    }
  }

  return maxSum;
}

// Example usage:
const array = [2, 4, 6, 8, 1, 3, 5, 7, 9];
const windowSize = 3;

const maxSum = maxSumSubarray(array, windowSize);
console.log(`Maximum sum of ${windowSize}-size window: ${maxSum}`);
```

Optimised

```js
function maxSumSubarray(arr, windowSize) {
  if (windowSize > arr.length) {
    return null; // Window size is larger than the array length
  }

  let maxSum = 0;
  let currentSum = 0;

  // Calculate the initial sum of the first window
  for (let i = 0; i < windowSize; i++) {
    maxSum += arr[i];
  }

  currentSum = maxSum;
  console.log(currentSum);
  let k = windowSize
  console.log(k);

  // Slide the window and calculate the maximum sum
  for (let i = windowSize; i < arr.length; i++) {
    currentSum = currentSum + arr[i] - arr[i - windowSize];
    maxSum = Math.max(maxSum, currentSum);
  }

  return maxSum;
}

// Example usage:
const array = [2, 4, 6, 8, 1, 3, 5, 7, 9];
const windowSize = 3;

const maxSum = maxSumSubarray(array, windowSize);
console.log(`Maximum sum of ${windowSize}-size window: ${maxSum}`);
```

