## Finding Floor and Ceiling in a Sorted Array

The `findFloor` and `findCeil` functions find the floor (largest element <= x) and ceiling (smallest element >= x) values in a sorted array.

```javascript
function findFloor(arr, n, x) {
    let low = 0, high = n - 1;
    let ans = -1;

    while (low <= high) {
        let mid = Math.floor((low + high) / 2);

        if (arr[mid] <= x) {
            ans = arr[mid];
            low = mid + 1; // Look for a larger index on the left
        } else {
            high = mid - 1; // Look on the right
        }
    }
    return ans;
}

function findCeil(arr, n, x) {
    let low = 0, high = n - 1;
    let ans = -1;

    while (low <= high) {
        let mid = Math.floor((low + high) / 2);

        if (arr[mid] >= x) {
            ans = arr[mid];
            high = mid - 1; // Look for a smaller index on the left
        } else {
            low = mid + 1; // Look on the right
        }
    }
    return ans;
}

// Example usage
const sortedArray = [1, 4, 6, 8, 10, 12, 14];
const value = 7;
const n = sortedArray.length;

const floorResult = findFloor(sortedArray, n, value);
console.log(`The largest element in the array <= ${value} is ${floorResult}`);

const ceilResult = findCeil(sortedArray, n, value);
console.log(`The smallest element in the array >= ${value} is ${ceilResult}`);
