## Binary Search Algorithm

In the algorithm, in every step, we are basically dividing the search space into 2 equal halves. This is actually equivalent to dividing the size of the array by 2, every time. After a certain number of divisions, the size will reduce to such an extent that we will not be able to divide that anymore, and the process will stop. The number of total divisions will be equal to the time complexity.

### Mathematical Derivation of Time Complexity

Let’s derive the number of divisions mathematically,

- If a number n can be divided by 2 for x times:
    - 2 ^ x = n

Therefore, x = logn (base is 2)

So the overall time complexity is O(logN), where N = size of the given array.

### Binary Search Implementation (Iterative)

```javascript
const binarySearchIterative = (a, n, target) => {
    var low = 0;
    var high = n - 1;
    var mid = 0;
    while (low <= high) {
        mid = Math.floor((low + high) / 2);

        if (a[mid] == target) return mid;
        else if (target > a[mid]) low = mid + 1;
        else high = mid - 1;
    }
    return -1;
}

let arr = [1, 3, 5, 6, 7, 12, 16];
let n = arr.length;

console.log(binarySearchIterative(arr, n, 3)); // Output: 1 (Index of the target element)
```

## Using Recursion

```javascript
const binarySearch = (a, low, high, target) => {
    if (low > high) return -1;
    var mid = Math.floor((low + high) / 2);
    if (target == a[mid]) return mid;
    else if (target > a[mid]) low = mid + 1;
    else high = mid - 1;
    return binarySearch(a, low, high, target);
}

let arr = [1, 3, 5, 6, 7, 12, 16];
let n = arr.length;

console.log(binarySearch(arr, 0, n - 1, 5));
```