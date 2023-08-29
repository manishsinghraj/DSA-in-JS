## Rotate Array by K Elements

**Problem Statement:** Given an array of integers, rotate the array of elements by k positions either to the left or to the right.


#### Example 1:
**Input:** N = 7, array[] = {1, 2, 3, 4, 5, 6, 7}, k = 2 (right rotation)
**Output:** 6, 7, 1, 2, 3, 4, 5
**Explanation:** The array is rotated to the right by 2 positions.

#### Example 2:
**Input:** N = 6, array[] = {3, 7, 8, 9, 10, 11}, k = 3 (left rotation)
**Output:** 9, 10, 11, 3, 7, 8
**Explanation:** The array is rotated to the left by 3 positions.

### Approach (Brute Force):

- Create a temporary array to store the first k elements.
- Shift the remaining elements in the original array to the left by k positions.
- Copy the elements from the temporary array back to the end of the original array.

**Time Complexity:** O(3N)
**Space Complexity:** O(K) - Uses extra space for the temporary array.

```javascript
const shiftArrByK = (a, n, k) => {
    var temp = [];
    for (let i = 0; i < k; i++) {
        temp.push(a[i]);
    }

    for (let i = k; i < n; i++) {
        a[i - k] = a[i];
    }

    var j = 0;

    // for (let i = n - k; i < n; i++) {
    //     a[i] = temp[j++];
    // }

    //OR
    for (let i = n - k; i < n; i++) {
        a[i] = temp[i - (n - k)];
    }
    return a;
}

arr = [1, 2, 3, 4, 5, 6, 7];

console.log(shiftArrByK(arr, arr.length, 3));
```

## Rotate Array by K Elements (Optimal Solution)

**Problem Statement:** Given an array of integers `arr`, shift the elements in the array by `K` positions to the right.

**Approach:**

This optimal approach involves reversing the array in three steps:
1. Reverse the first `K` elements.
2. Reverse the remaining `N - K` elements.
3. Reverse the entire array.

By performing these three reverse operations, the array will be shifted by `K` positions to the right.

- **Time Complexity:** O(N)
  - The algorithm performs three reverse operations: O(K) + O(N - K) + O(N), which is effectively O(2N), but it simplifies to O(N) since we are only concerned about the dominant term.
- **Space Complexity:** O(1)
  - The algorithm uses a constant amount of extra space for variables.

```javascript
const shifElementbyK = (a, n, k) => {
    reverse(a, 0, k - 1);
    reverse(a, k, n - 1);
    reverse(a, 0, n - 1);
    return a;
}

const reverse = (a, startIndex, endIndex) => {
    while (startIndex <= endIndex) {
        var temp = a[startIndex];
        a[startIndex] = a[endIndex];
        a[endIndex] = temp;
        startIndex++;
        endIndex--;
    }
    return a;
}

let arr = [1, 2, 3, 4, 5, 6, 7];
let n = arr.length;
let k = 3;
console.log(shifElementbyK(arr, n, k));
```

## Rotate Array by K Elements (Using JavaScript Built-in Methods)

**Problem Statement:** Given an array of integers, rotate the array of elements by k positions either to the left or to the right.

### Approach (Using JavaScript Built-in Methods):

1. Calculate the effective value of k by taking its modulo with the length of the array.
2. Split the array into two parts: the first part contains elements from index 0 to n - k - 1, and the second part contains elements from index n - k to the end.
3. Concatenate the second part with the first part to obtain the rotated array.

```javascript
const shiftElementsByK = (a, k) => {
    const n = a.length;
    k %= n; // To handle cases where k is greater than the array length

    const firstPart = a.slice(0, n - k);
    const secondPart = a.slice(n - k);

    return secondPart.concat(firstPart);
};

const originalArray = [1, 2, 3, 4, 5, 6, 7];
const k = 3;
const shiftedArray = shiftElementsByK(originalArray, k);
console.log(shiftedArray); // Output: [5, 6, 7, 1, 2, 3, 4]
```

## Handling Cases Where k is Greater Than Array Length in Rotation

Sometimes, when rotating an array by a specific number of positions `k`, `k` might be larger than the array's length `n`. This scenario requires special handling to ensure that the rotation operation produces the desired outcome.

### The Modulo Operator Approach

To address cases where `k` exceeds the array length `n`, we can employ the modulo operator (`%`). The modulo operation yields the remainder when dividing `k` by `n`, effectively bringing `k` into the range of `[0, n-1]`.

This is essential because rotating an array by a multiple of its length results in the same array configuration. By using the modulo operator, we effectively normalize `k`, making it equivalent to a rotation by `k % n` positions.

Let's illustrate this through an example:

Assume we have:
- `k = 10`
- `n = 7`

Applying `k %= n` results in `k = 10 % 7 = 3`. Thus, rotating by 10 positions becomes equivalent to rotating by 3 positions due to the array's cyclical nature.

### Benefits of Using the Modulo Operator

By utilizing the modulo operation, we handle scenarios where `k` is greater than `n` gracefully, ensuring our rotation logic remains consistent and valid. This technique simplifies our code by bringing `k` within the array's valid index range.

In practical terms, when implementing rotation logic, such as in provided code snippets, applying `k %= n` before executing the rotation ensures predictable and correct outcomes regardless of the initial value of `k`.

```javascript
// Example code illustrating the use of modulo for rotation
const shiftElementsByK = (a, k) => {
    const n = a.length;
    k %= n; // Normalize k

    const firstPart = a.slice(0, n - k);
    const secondPart = a.slice(n - k);

    return secondPart.concat(firstPart);
};

const originalArray = [1, 2, 3, 4, 5, 6, 7];
const k = 10; // No longer an issue with modulo
const shiftedArray = shiftElementsByK(originalArray, k);
console.log(shiftedArray); // Correctly rotated array