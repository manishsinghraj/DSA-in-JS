## Union of Two Sorted Arrays

**Problem Statement:** Given two sorted arrays, `arr1` and `arr2`, of sizes `n` and `m`, find the union of two sorted arrays.

The union of two arrays can be defined as the set of common and distinct elements in the two arrays. Elements in the union should be in ascending order.

### Examples

#### Example 1:
**Input:**
- n = 5, m = 5.
- `arr1[]` = {1, 2, 3, 4, 5}
- `arr2[]` = {2, 3, 4, 4, 5}
**Output:**
- Union: {1, 2, 3, 4, 5}

#### Example 2:
**Input:**
- n = 10, m = 7.
- `arr1[]` = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
- `arr2[]` = {2, 3, 4, 4, 5, 11, 12}
**Output:**
- Union: {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12}

### Brute Force Approach using Set

**Time Complexity:** O((m + n) log(m + n))

- Inserting an element in a `Set` takes log(N) time, where N is the number of elements in the `Set`.
- At most, the `Set` can store m + n elements (when there are no common elements and elements in `arr1` and `arr2` are distinct).
- Inserting the m + n-th element takes log(m + n) time.
- On average, across inserting all elements in the worst case, it would take O((m + n) log(m + n)) time.

**Space Complexity:** O(m + n) (If the space of the union ArrayList is considered)
- The `Set` stores unique elements from both arrays.

**Space Complexity:** O(1) (If the space of the union ArrayList is not considered)

### Approach

- Create a `Set` to store unique elements from both arrays.
- Traverse through `arr1` and add its elements to the `Set`.
- Traverse through `arr2` and add its elements to the `Set`.
- Create an empty `union` ArrayList.
- Convert the `Set` to an iterator using `set.values()`.
- Traverse through the iterator and push its values to the `union` ArrayList.

```javascript
function findUnion(arr1, arr2) {
    const set = new Set();
    const union = [];

    for (let i = 0; i < arr1.length; i++) {
        set.add(arr1[i]);
    }

    for (let i = 0; i < arr2.length; i++) {
        set.add(arr2[i]);
    }

    const setIterator = set.values(); // Get an iterator for the Set

    for (let i = 0; i < set.size; i++) {
        union.push(setIterator.next().value);
    } // OR

    // for (let num of set) {
    //     union.push(num);
    // }

    return union;
}

const arr1 = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const arr2 = [2, 3, 4, 4, 5, 11, 12];

const union = findUnion(arr1, arr2);

console.log("Union of arr1 and arr2 is:");
console.log(...union);
```
## Union of Two Sorted Arrays (Optimal Solution)

**Problem Statement:** Given two sorted arrays, `arr1` and `arr2`, of sizes `n` and `m`, find the union of two sorted arrays.

### Optimal Approach

- **Time Complexity:** O(n + m)
  - The algorithm traverses both arrays once, where `n` is the length of `arr1` and `m` is the length of `arr2`. The time complexity is directly proportional to the sum of the lengths of the arrays.

- **Space Complexity:** O(n + m)
  - The additional space required includes the `union` array to store the final result. In the worst case, where all elements are distinct, the `union` array can have up to `n + m` elements.

- Initialize two pointers `i` and `j` to keep track of the current elements in `arr1` and `arr2` respectively.
- Initialize an empty array `union` to store the union of the two arrays.
- Traverse through both arrays while comparing the elements:
  - If the element at `arr1[i]` is less than or equal to the element at `arr2[j]`, add `arr1[i]` to the `union` array.
  - If the element at `arr2[j]` is less than the element at `arr1[i]`, add `arr2[j]` to the `union` array.
- Handle cases where the elements are duplicates by checking if the current element is different from the last element in the `union` array before adding it.
- After traversing both arrays, if there are any remaining elements in `arr1`, add them to the `union` array.
- If there are any remaining elements in `arr2`, add them to the `union` array.
- Return the `union` array.

```javascript
function findUnion(arr1, arr2) {
  let i = 0, j = 0; // Pointers
  let union = []; // Union array

  while (i < arr1.length && j < arr2.length) {
    if (arr1[i] <= arr2[j]) { // Case 1 and 2
      if (union.length === 0 || union[union.length - 1] !== arr1[i])
        union.push(arr1[i]);
      i++;
    } else { // Case 3
      if (union.length === 0 || union[union.length - 1] !== arr2[j])
        union.push(arr2[j]);
      j++;
    }
  }

  while (i < arr1.length) { // If any elements left in arr1
    if (union[union.length - 1] !== arr1[i])
      union.push(arr1[i]);
    i++;
  }

  while (j < arr2.length) { // If any elements left in arr2
    if (union[union.length - 1] !== arr2[j])
      union.push(arr2[j]);
    j++;
  }

  return union;
}

const arr1 = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const arr2 = [2, 3, 4, 4, 5, 11, 12];

const union = findUnion(arr1, arr2);

console.log("Union of arr1 and arr2 is:");
console.log(union.join(" "));
```