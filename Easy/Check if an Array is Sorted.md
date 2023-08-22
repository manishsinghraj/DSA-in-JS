## Check if an Array is Sorted

**Problem Statement:** Given an array of size n, write a program to check if the given array is sorted in ascending (increasing or non-decreasing) order or not. If the array is sorted, return True. Otherwise, return False. Note that two consecutive equal values are considered sorted.

#### Example 1:
**Input:** N = 5, array[] = {1, 2, 3, 4, 5}
**Output:** True.
**Explanation:** The given array is sorted, as every element in the array is smaller than or equal to its next values. Thus, the answer is True.

#### Example 2:
**Input:** N = 5, array[] = {5, 4, 6, 7, 8}
**Output:** False.
**Explanation:** The given array is not sorted, as every element in the array is not smaller than or equal to its next values. Therefore, the answer is False. Element 5 is not smaller than or equal to its future elements.

### Approach 1:
1. Consider the first element as the smallest.
2. Traverse through the array.
3. If any element is found to be less than the selected element, then the array is not sorted, and the function returns false.

**Time Complexity:** O(N)
**Space Complexity:** O(1)

```javascript
const isSorted = (arr) => {
    let smallest = arr[0];
    let isSorted = true;

    for (let i = 1; i < arr.length; i++) {
        if (arr[i] < smallest) {
            isSorted = false;
            break;
        } else {
            smallest = arr[i];
        }
    }

    return isSorted;
}

console.log(isSorted([1, 3, 4, 4, 5, 8]));
```

### Approach 2:

1. Iterate through the array from the second element.
2. If any element is less than its previous element, the array is not sorted, and the function returns false.

**Time Complexity:** O(N)
**Space Complexity:** O(1)

```javascript
const isSorted2 = (arr) => {
    for (let i = 1; i < arr.length; i++) {
        if (arr[i] < arr[i - 1]) return false;
    }
    return true;
}

console.log(isSorted2([1, 3, 4, 2, 5, 8]));
