## Find the Largest Element in an Array

### Example 1:
**Input:** `arr[] = { 2, 5, 1, 3, 0};`  
**Output:** 5  
**Explanation:** 5 is the largest element in the array.

### Example 2:
**Input:** `arr[] = { 8, 10, 5, 7, 9};`  
**Output:** 10  
**Explanation:** 10 is the largest element in the array.

### Brute Force Approach:
1. Sort the array.
2. Print the last element, i.e., `arr[n-1]`.
   - **Time Complexity (TC):** O(N log N);
   - **Space Complexity (SC):** O(1);

```javascript
const largestElement1 = (arr) => {
    arr.sort((a, b) => { return a - b });
    console.log(arr[arr.length - 1]);
}

largestElement1([1, 3, 52, 8, 3]);
```


## Optimal Solution

1. Consider the first element as the largest.
2. Use a `for` loop to traverse through the rest of the elements and compare if the current element is less than the current largest.
3. Update the current largest with the previous value if a larger element is found.
4. Print the largest element.
   - **Time Complexity (TC):** O(N);
   - **Space Complexity (SC):** O(1);

```javascript
const largestElement2 = (arr) => {
    let largest = arr[0];
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] > largest) {
            largest = arr[i];
        }
    }
    return largest;
}

console.log(largestElement2([3, 5, 21, 1, 8]));
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