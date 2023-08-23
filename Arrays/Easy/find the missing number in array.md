## Find the Missing Number in an Array

**Problem Statement:** Given an integer N and an array of size N-1 containing N-1 numbers between 1 to N. Find the number (between 1 to N), that is not present in the given array.

**Example 1:**
Input Format: N = 5, array[] = {1, 2, 4, 5}
Result: 3
Explanation: In the given array, number 3 is missing. So, 3 is the answer.

**Example 2:**
Input Format: N = 3, array[] = {1, 3}
Result: 2
Explanation: In the given array, number 2 is missing. So, 2 is the answer.

### BruteForce Approach
### Algorithm (Using Hash Map)

- **Time Complexity:** O(N) + O(N) ~ O(2*N), where N = size of the array + 1.
  - For storing the frequencies in the hash array, the program takes O(N) time complexity.
  - For checking the frequencies in the second step, again O(N) time complexity is required. So, the total time complexity is O(N) + O(N).

- **Space Complexity:** O(N), where N = size of the array + 1.
  - An extra hash array of size N+1 is used.

```javascript
function missingNumber(a, N) {
  const hash = new Array(N + 1).fill(0); // hash array

  // storing the frequencies:
  for (let i = 0; i < N - 1; i++) {
    hash[a[i]]++;
  }

  // checking the frequencies for numbers 1 to N:
  for (let i = 1; i <= N; i++) {
    if (hash[i] === 0) {
      return i;
    }
  }

  // The following line will never execute.
  // It is just to avoid warnings.
  return -1;
}

function main() {
  const N = 5;
  const a = [1, 2, 4, 5];
  const ans = missingNumber(a, N);
  console.log("The missing number is:", ans);
}

main();

```
### Better Approach
- **Time Complexity:** O(N), where N is the size of the array.
  - The algorithm only iterates through the array once.

- **Space Complexity:** O(1)
  - The algorithm uses a constant amount of extra space for variables.

```javascript
const findMissingNumb = (a, n) => {
    for (let i = 1; i <= n; i++) {
        if (a[i - 1] !== i) {
            return i;
        }
    }
    return -1;
}

let arr = [1, 2, 5];
let n = arr.length;

console.log(findMissingNumb(arr, n));

```

## Find the Missing Number in an Array (Optimal Approach 1)

**Optimal Approach 1:**

In this approach, we utilize the sum of the first N natural numbers formula to find the missing number. We calculate the expected sum of all numbers from 1 to N, and then subtract the sum of the elements in the given array. The result will be the missing number.

- **Time Complexity:** O(N), where N is the size of the array + 1.
  - The algorithm runs a single loop through the array of size N-1 to calculate the sum of array elements.
  - The summation formula takes constant time.

- **Space Complexity:** O(1)
  - The algorithm uses a constant amount of extra space for variables.

```javascript
function missingNumber(a, N) {
  // Summation of first N numbers:
  const summation = (N * (N + 1)) / 2;

  // Summation of all array elements:
  let s2 = 0;
  for (let i = 0; i < N - 1; i++) {
    s2 += a[i];
  }

  const missingNum = summation - s2;
  return missingNum;
}

function main() {
  const N = 5;
  const a = [1, 2, 4, 5];
  const ans = missingNumber(a, N);
  console.log("The missing number is:", ans);
}

main();
```
## Find the Missing Number in an Array (Optimal Approach 2 - XOR-based)

**Optimal Approach 2 (XOR-based):**

This approach utilizes the XOR operation to find the missing number. By XOR-ing all the numbers from 1 to N and XOR-ing all the elements in the array, the XOR of these two results will give the missing number.

- **Time Complexity:** O(N), where N is the size of the array + 1.
  - The algorithm iterates through the array once and performs XOR operations.

- **Space Complexity:** O(1)
  - The algorithm uses a constant amount of extra space for variables.

**Note:** The XOR-based solution is often preferred due to its elegance, better memory efficiency, and lack of potential for integer overflow issues when dealing with large numbers.

```javascript
const findMissingNumb = (a, n) => {
    var xor1 = 0;
    for (let i = 1; i <= n; i++) {
        xor1 = xor1 ^ i;
    }

    var xor2 = 0;
    for (let i = 0; i < n; i++) {
        xor2 = xor2 ^ a[i];
    }

    return xor1 ^ xor2;
}

let arr = [1, 3, 5, 8];
let n = arr.length;

console.log(findMissingNumb(arr, n));
```