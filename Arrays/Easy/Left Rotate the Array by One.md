## Left Rotate the Array by One

**Problem Statement:** Given an array of N integers, left rotate the array by one place.


#### Example 1:
**Input:** N = 5, array[] = {1, 2, 3, 4, 5}
**Output:** 2, 3, 4, 5, 1
**Explanation:** All the elements in the array will be shifted towards the left by one, so '2' will now become the first index, and '1' which was present at the first index will be shifted to the last.

#### Example 2:
**Input:** N = 1, array[] = {3}
**Output:** 3
**Explanation:** Here, there's only one element present. The element at the first index will be shifted to the last index, which is also the first index.

### Approach (Brute Force):

1. Create a temporary array to store the rotated elements.
2. Iterate through the original array from index 1 and copy elements to the temporary array.
3. Place the element at index 0 at the end of the temporary array.
4. Print the elements of the temporary array.

**Time Complexity:** O(N)
**Space Complexity:** O(N)

```javascript
function shiftArrBy1(arr, n) {
  let temp = new Array(n);
  for (let i = 1; i < n; i++) {
    temp[i - 1] = arr[i];
  }
  temp[n - 1] = arr[0];
  for (let i = 0; i < n; i++) {
    console.log(temp[i] + " ");
  }
  console.log();
}

let n = 5;
let arr = [1, 2, 3, 4, 5];
shiftArrBy1(arr, n);
```

## (Optimal Solution)

**Problem Statement:** Given an array of N integers, left rotate the array by one place.

### Optimal Approach:

- **Time Complexity:** O(N)
- **Space Complexity:** O(1) is the space, but if it is asked in the algorithm, it is O(N) as we are modifying the existing given array.

```javascript
const shiftArrBy1 = (a, n) => {
    let temp = a[0];

    for (let i = 1; i < n; i++) {
        a[i - 1] = a[i];
    }
    a[n - 1] = temp;
    return a;
}

const arr = [5, 3, 7, 8, 9, 2, 3];

console.log(shiftArrBy1(arr, arr.length));
```





