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

