## Two Sum: Check if a Pair with Given Sum Exists in Array

### Problem Statement
Given an array of integers `arr[]` and an integer `target`.

**1st variant:** Return "YES" if there exist two numbers such that their sum is equal to the target. Otherwise, return "NO".

**2nd variant:** Return indices of the two numbers such that their sum is equal to the target. Otherwise, return `[-1, -1]`.

#### Example 1:
**Input Format:** N = 5, `arr[] = [2, 6, 5, 8, 11]`, `target = 14`  
**Result:** "YES" (for 1st variant)  
**Result:** `[1, 3]` (for 2nd variant)  
**Explanation:** `arr[1] + arr[3] = 14`. So, the answer is "YES" for the first variant and `[1, 3]` for the 2nd variant.

#### Example 2:
**Input Format:** N = 5, `arr[] = [2, 6, 5, 8, 11]`, `target = 15`  
**Result:** "NO" (for 1st variant)  
**Result:** `[-1, -1]` (for 2nd variant)  
**Explanation:** There exist no such two numbers whose sum is equal to the target.

### Brute Force
**Time Complexity:** O(N^2), where N is the size of the array.  
**Reason:** There are two nested loops, each running for approximately N times.

**Space Complexity:** O(1) as we are not using any extra space.

```javascript
const twoSum = (a, n, k) => {
    for (let i = 0; i < n; i++) {
        for (let j = i + 1; j < n; j++) {
            if (a[i] + a[j] == k) {
                console.log(i, j);
                return true;
            }
        }
    }
    console.log(-1, -1);
    return false;
}

let arr = [2, 6, 5, 8, 11];
var n = arr.length;
var k = 1;
console.log(twoSum(arr, n, k));

```

## Better Approach

**Time Complexity:** O(N), where N is the size of the array.
**Reason:** The loop runs N times in the worst case, and searching in a hashmap takes O(1) generally. So the time complexity is O(N).

*Note*: In the worst case (which rarely happens), the `unordered_map` takes O(N) to find an element. In that case, the time complexity will be O(N^2). If we use `map` instead of `unordered_map`, the time complexity will be O(N * logN) as the `map` data structure takes logN time to find an element.

**Space Complexity:** O(N) as we use the map data structure.

*Note*: We have optimized this problem significantly. However, if in an interview, we are not allowed to use the map data structure, then we should consider the following approach, i.e., the two-pointer approach. This approach will have the same time complexity as the better approach.

```javascript
const twoSum = (a, n, target) => {
    const map = new Map();
    for (let i = 0; i < n; i++) {
        const moreNeeded = target - a[i];
        if (map.has(moreNeeded)) {
            console.log([map.get(moreNeeded)], i);
            return true;
        } else {
            map.set(a[i], i);
        }
    }
    return false;
}

let arr = [2, 6, 5, 8, 11];
var n = arr.length;
var k = 14;
console.log(twoSum(arr, n, k));
```

## Optimal Approach

**Output:** This is the answer for variant 1: YES

*Note*: For variant 2, we can store the elements of the array along with their indices in a new array. Then the rest of the code will be similar. When returning, we need to return the stored indices instead of returning "YES". However, for this variant, the recommended approach is approach 2, i.e., the hashing approach.

**Time Complexity:** O(N) + O(N * logN), where N is the size of the array.
**Reason:** The loop will run at most N times. Sorting the array will take N * logN time complexity.

**Space Complexity:** O(1) as we are not using any extra space.

*Note*: Here we are modifying the given array in place. If we need to consider this change, the space complexity will be O(N).

```javascript
function twoSum(n, arr, target) {
    arr.sort((a, b) => a - b);
    let left = 0;
    let right = n - 1;
    while (left < right) {
        const sum = arr[left] + arr[right];
        if (sum === target) {
            return "YES";
        } else if (sum < target) {
            left++;
        } else {
            right--;
        }
    }
    return "NO";
}

const n = 5;
const arr = [2, 6, 5, 8, 11];
const target = 14;
const ans = twoSum(n, arr, target);
console.log("This is the answer for variant 1:", ans);
```

## Optimal Approach using Dutch National Flag Algorithm

**Time Complexity:** O(N), where N is the size of the given array.
**Reason:** We are using a single loop that can run at most N times.

**Space Complexity:** O(1) as we are not using any extra space.

```javascript
const sortGivenNumbers = (a, n) => {
    var low = 0;
    var mid = 0;
    var high = n - 1;

    while (mid <= high) {
        if (a[mid] == 0) {
            [a[low], a[mid]] = [a[mid], a[low]];
            low++;
            mid++;
        } else if (a[mid] == 1) {
            mid++;
        } else {
            [a[mid], a[high]] = [a[high], a[mid]];
            high--;
        }
    }
    return a;
}

let arr = [0, 1, 1, 2, 2, 0, 0, 1, 2, 0];
var n = arr.length;

console.log(sortGivenNumbers(arr, n));
```

