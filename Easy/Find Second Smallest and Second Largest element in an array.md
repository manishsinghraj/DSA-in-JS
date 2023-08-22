## Find Second Smallest and Second Largest Element in an Array
**Problem Statement:** Given an array, find the second smallest and second largest element in the array. Print ‘-1’ in the event that either of them doesn’t exist.

### Example 1:
**Input:** `[1, 2, 4, 7, 7, 5]`
**Output:**
Second Smallest: 2
Second Largest: 5
**Explanation:** The elements are 1, 2, 4, 7, 7, 5. The second largest of these is 5, and the second smallest is 2.

### Example 2:
**Input:** `[1]`
**Output:**
Second Smallest: -1
Second Largest: -1
**Explanation:** Since there is only one element in the array, it is both the largest and smallest element. There is no second largest or second smallest element present.

### Brute Force Approach:
1. Sort the array in ascending order.
2. Get the last element as the largest.
3. Iterate through the array from the end and find the second largest by skipping duplicates of the largest element.

   - **Time Complexity:** O(N log N) for sorting + O(N) for traversing = O(N log N) + O(N)
   - **Space Complexity:** O(1)

```javascript
const secondLargest1 = (arr) => {
    let n = arr.length;
    arr.sort((a, b) => (a - b));
    let largest = arr[n - 1];
    let secondLargest = -1;

    for (let i = n - 2; i >= 0; i--) {
        if (arr[i] !== largest) {
            secondLargest = arr[i];
            break;
        }
    }
    return secondLargest;
}

console.log(secondLargest1([2, 3, 6, 5, 1]))
```

## Better Solution

**Approach:**
1. First pass to find the largest element.
2. Second pass to find the second largest element with a condition.

**Time Complexity:** O(N) + O(N) = O(2N)
**Space Complexity:** O(1)

```javascript
const secondLargest2 = (arr) => {
    let n = arr.length;
    let largest = arr[0];
    let secondLargest = -1;

    // First pass to find the largest element
    for (let i = 0; i < n; i++) {
        if (arr[i] > largest) {
            largest = arr[i];
        }
    }

    // Second pass to find the second largest element
    for (let i = n - 1; i >= 0; i--) {
        if (arr[i] > secondLargest && arr[i] !== largest) {
            secondLargest = arr[i];
        }
    }
    return secondLargest;
}

console.log(secondLargest2([2, 3, 6, 5, 1]))
```

## Optimal Solution

**Approach:**
- For finding the second smallest:
  1. Initialize `small` and `second_small` with Infinity.
  2. Iterate through the array and update `small` and `second_small` accordingly.
- For finding the second largest:
  1. Initialize `large` and `second_large` with -Infinity.
  2. Iterate through the array and update `large` and `second_large` accordingly.

**Time Complexity:** O(N) for both finding the second smallest and the second largest
**Space Complexity:** O(1)

```javascript
function secondSmallest(arr) {
    if (arr.length < 2)
        return -1;

    let small = Infinity;
    let second_small = Infinity;

    for (let i = 0; i < arr.length; i++) {
        if (arr[i] < small) {
            second_small = small;
            small = arr[i];
        } else if (arr[i] < second_small && arr[i] !== small) {
            second_small = arr[i];
        }
    }

    return second_small;
}

function secondLargest(arr) {
    if (arr.length < 2)
        return -1;

    let large = -Infinity;
    let second_large = -Infinity;

    for (let i = 0; i < arr.length; i++) {
        if (arr[i] > large) {
            second_large = large;
            large = arr[i];
        } else if (arr[i] > second_large && arr[i] !== large) {
            second_large = arr[i];
        }
    }

    return second_large;
}

const arr = [1, 2, 4, 7, 7, 5];
const sS = secondSmallest(arr);
const sL = secondLargest(arr);

console.log("Second smallest is " + sS);
console.log("Second largest is " + sL);

```

### Inbuilt method
```javascript
function secondSmallest(arr) {
    if (arr.length < 2)
        return -1;

    const sortedArr = arr.slice().sort((a, b) => a - b);

    let second_small = sortedArr.find(element => element !== sortedArr[0]);

    return second_small === undefined ? -1 : second_small;
}

function secondLargest(arr) {
    if (arr.length < 2)
        return -1;

    const sortedArr = arr.slice().sort((a, b) => b - a);

    let second_large = sortedArr.find(element => element !== sortedArr[0]);

    return second_large === undefined ? -1 : second_large;
}

const arr = [1, 2, 4, 7, 7, 5];
const sS = secondSmallest(arr);
const sL = secondLargest(arr);

console.log("Second smallest is " + sS);
console.log("Second largest is " + sL);
```
### Time Complexity:

- The time complexity of the `sort` method is O(n * log n), where n is the length of the array.
- The `find` method adds O(n) complexity for locating the second smallest and second largest elements.
- Therefore, the overall time complexity for both `secondSmallest` and `secondLargest` functions is O(n * log n) + O(n), which simplifies to O(n * log n).

### Space Complexity:

- The space complexity is O(n) due to the usage of the `sortedArr` array, which is a copy of the input array.

In this solution, the code creates a sorted copy of the input array using the `sort` method. The `find` method is then used to locate the second smallest and second largest elements, while skipping any duplicates of the smallest or largest element found at the beginning of the sorted array. Although the use of JavaScript inbuilt methods simplifies the code, the overall time complexity remains higher due to the sorting operation.





