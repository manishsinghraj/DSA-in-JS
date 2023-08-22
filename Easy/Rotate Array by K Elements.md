## Rotate Array by K Elements

**Problem Statement:** Given an array of integers, rotate the array of elements by k positions either to the left or to the right.

### Examples

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

**Problem Statement:** Given an array of integers, rotate the array of elements by k positions either to the left or to the right.

### Optimal Approach:

- Reverse the first k elements of the array.
- Reverse the remaining n-k elements of the array.
- Reverse the entire array.

**Time Complexity:** O(N)
**Space Complexity:** O(1)

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