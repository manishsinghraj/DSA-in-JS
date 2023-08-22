## Linear Search

**Problem Statement:** Given an array and an element `num`, the task is to find if `num` is present in the given array. If present, print the index of the element; otherwise, print -1.

### Examples

#### Example 1:
**Input:** arr[] = 1, 2, 3, 4, 5, `num` = 3
**Output:** 2
**Explanation:** 3 is present at the 2nd index.

#### Example 2:
**Input:** arr[] = 5, 4, 3, 2, 1, `num` = 5
**Output:** 0
**Explanation:** 5 is present at the 0th index.

### Approach (Linear Search):

- Traverse through the array.
- For each element encountered, check if it matches `num`.
- If a match is found, return the index.
- If no match is found after traversing the entire array, return -1.

**Time Complexity:** O(N)
**Space Complexity:** O(1)

```javascript
const linearSearch = (a, n) => {
    for (let i = 0; i < a.length; i++) {
        if (a[i] == n) {
            return i;
        }
    }
    return -1;
}

let arr = [1, 2, 3, 4, 5, 6];
console.log(linearSearch(arr, 10));
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