## Moving Zeros to the End of the Array

**Problem Statement:** Given an array of integers, the task is to move all zeros to the end of the array while maintaining the order of non-negative integers at the front.


#### Example 1:
**Input:** 1, 0, 2, 3, 0, 4, 0, 1
**Output:** 1, 2, 3, 4, 1, 0, 0, 0
**Explanation:** All the zeros are moved to the end, and non-negative integers are moved to the front while maintaining their order.

#### Example 2:
**Input:** 1, 2, 0, 1, 0, 4, 0
**Output:** 1, 2, 1, 4, 0, 0, 0
**Explanation:** All the zeros are moved to the end, and non-negative integers are moved to the front while maintaining their order.

### Approach (Brute Force):

- Create a temporary array to store non-zero elements.
- Traverse through the original array and push non-zero elements to the temporary array.
- Count the number of non-zero elements and fill the remaining positions with zeros.
- Assign the values of the temporary array back to the original array.

**Time Complexity:** O(N)
**Space Complexity:** O(x), where x is the number of non-zero elements.

```javascript
const moveZerosToEnd = (a, n) => {
    var temp = [];
    for (let i = 0; i < n; i++) {
        if (a[i] !== 0) {
            temp.push(a[i]);
        }
    }
    for (let i = temp.length; i < n; i++) {
        temp[i] = 0;
    }
    return temp;
}

let arr = [1, 0, 2, 3, 2, 0, 0, 4, 5, 1];
let n = arr.length;

console.log(moveZerosToEnd(arr, n));
```

## Moving Zeros to the End of the Array (Optimal Approach)

### Approach (Optimal):

- Initialize a pointer `j` to -1.
- Traverse through the array to find the index of the first zero encountered. Set `j` to this index.
- If no zero is found (`j` remains -1), the array has no zeros, and it's already in the desired order, so return the array.
- Traverse the array again, starting from the index next to `j`.
- For each non-zero element encountered, swap it with the element at index `j` and increment `j`.
- This approach maintains the order of non-negative integers while effectively moving zeros to the end.

**Time Complexity:** O(N)
**Space Complexity:** O(1)

```javascript
const moveZerosToEnd = (a, n) => {
    let j = -1;
    for (let i = 0; i < n; i++) {
        if (a[i] == 0) {
            j = i;
            break;
        }
    }

    if (j == -1) return a;

    for (let i = j + 1; i < n; i++) {
        if (a[i] !== 0) {
            [a[i], a[j]] = [a[j], a[i]]; // Swap elements
            j++;
        }
    }
    return a;
}

let arr = [1, 0, 2, 3, 2, 0, 0, 4, 5, 1];
let n = arr.length;

console.log(moveZerosToEnd(arr, n));
``` 

## Moving Zeros to the End of the Array (Using Inbuilt Method)

### Approach (Using Inbuilt Method):

- Utilize the `filter` method to create a new array containing only non-zero elements.
- Calculate the count of zeros in the original array by subtracting the length of the new non-zero elements array from the original array length.
- Use the `concat` method to concatenate the non-zero elements array with an array of zeros (created using `Array(zeroCount).fill(0)`), effectively placing the zeros at the end.

```javascript
const moveZerosToEnd = (a) => {
    const nonZeroElements = a.filter(element => element !== 0);
    const zeroCount = a.length - nonZeroElements.length;
    return nonZeroElements.concat(Array(zeroCount).fill(0));
};

let arr = [1, 0, 2, 3, 2, 0, 0, 4, 5, 1];
console.log(moveZerosToEnd(arr));