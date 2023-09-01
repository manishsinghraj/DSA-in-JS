## Lower Bound Binary Search

In a lower bound binary search, you do the following:

- If the current element is greater than or equal to the target, you move to the left side of the array (end = mid - 1).
- If the current element is less than the target, you move to the right side of the array (start = mid + 1).

```javascript
const lowerBound = (a, n, target) => {
    var low = 0;
    var high = n - 1;
    var ans = n;

    while (low <= high) {
        var mid = Math.floor((low + high) / 2);
        if (a[mid] >= target) {
            ans = mid;
            high = mid - 1;
        } else {
            low = mid + 1;
        }
    }

    return a[ans];
}

let arr = [1, 3, 5, 6, 7, 12, 16];
let n = arr.length;

console.log(lowerBound(arr, n, 7)); // Output: 7
