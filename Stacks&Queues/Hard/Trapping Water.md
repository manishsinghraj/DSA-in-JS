## Trapping Water

### Brute Force Approach
### Time Complexity: O(N^2)
### Space Complexity: O(1)

```javascript
function trap(arr) {
    const n = arr.length;
    let waterTrapped = 0;

    for (let i = 0; i < n; i++) {
        let j = i;
        let leftMax = 0;
        let rightMax = 0;

        // Calculate the maximum height to the left of the current element
        while (j >= 0) {
            leftMax = Math.max(leftMax, arr[j]);
            j--;
        }

        j = i;

        // Calculate the maximum height to the right of the current element
        while (j < n) {
            rightMax = Math.max(rightMax, arr[j]);
            j++;
        }

        // Calculate the water trapped at the current element
        waterTrapped += Math.min(leftMax, rightMax) - arr[i];
    }

    return waterTrapped;
}

const arr = [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1];
console.log(`The water that can be trapped is ${trap(arr)}`);
```

## Trapping Water (Improved)

### Time Complexity: O(N) + O(N) + O(N) = O(N)
### Space Complexity: O(2N) = O(N)

```javascript
function trap(arr) {
    const n = arr.length;
    const prefix = new Array(n).fill(0);
    const suffix = new Array(n).fill(0);

    // Calculate the maximum height to the left of each element and store it in the prefix array
    prefix[0] = arr[0];
    for (let i = 1; i < n; i++) {
        prefix[i] = Math.max(prefix[i - 1], arr[i]);
    }

    // Calculate the maximum height to the right of each element and store it in the suffix array
    suffix[n - 1] = arr[n - 1];
    for (let i = n - 2; i >= 0; i--) {
        suffix[i] = Math.max(suffix[i + 1], arr[i]);
    }

    let waterTrapped = 0;

    // Calculate the water trapped at each element by taking the minimum of the left and right maximum heights
    for (let i = 0; i < n; i++) {
        waterTrapped += Math.min(prefix[i], suffix[i]) - arr[i];
    }

    return waterTrapped;
}

const arr = [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1];
console.log(`The water that can be trapped is ${trap(arr)}`);
