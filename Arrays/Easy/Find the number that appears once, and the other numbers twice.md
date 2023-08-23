## Find the Number that Appears Once

**Problem Statement:** Given a non-empty array of integers `arr`, every element appears twice except for one. Find that single one.

**Example 1:**

Input: `arr = [2, 2, 1]`
Result: 1
Explanation: In this array, only the element 1 appears once, and so it is the answer.

**Example 2:**

Input: `arr = [4, 1, 2, 1, 2]`
Result: 4
Explanation: In this array, only the element 4 appears once, and the other elements appear twice. So, 4 is the answer.

- **Brute Force Approach:**
  - **Time Complexity:** O(N^2)
    - Two nested loops are used to compare each element with every other element in the array.
  - **Space Complexity:** O(1)
    - The algorithm uses a constant amount of extra space for variables.

```javascript
const numberAppearOnes = (a, n) => {
    var num = 0;
    for (let i = 0; i < n; i++) {
        num = a[i];
        var count = 0;
        for (let j = 0; j < n; j++) {
            if (a[j] == num) {
                count++;
            }
        }
        if (count == 1) {
            return num;
        }
    }
}

let arr = [1, 1, 2, 2, 3, 3, 4, 4, 5, 6, 6];
console.log(numberAppearOnes(arr, arr.length));
```

## Find the Number that Appears Once (Better Approach)

**Problem Statement:** Given a non-empty array of integers `arr`, every element appears twice except for one. Find that single one.

**Better Approach:**

This approach involves using a hash table to count the occurrences of each element in the array. It first finds the maximum element in the array to determine the size of the hash table. Then, it iterates through the array to populate the hash table with element counts. Finally, it searches the hash table for the element with a count of 1, which is the single element that appears once.

- **Time Complexity:** O(N) + O(N) + O(N), where N is the size of the array.
  - The first O(N) is for finding the maximum element.
  - The second O(N) is to populate the hash table.
  - The third O(N) is to search the hash table for the single element.
- **Space Complexity:** O(maxElement + 1), where maxElement is the maximum element of the array.

```javascript
const numberAppearOnes = (a, n) => {
    var max = 0;
    for (let i = 0; i < n; i++) {
        max = Math.max(max, a[i]);
    }

    var hash = new Array(max + 1).fill(0);

    for (let i = 0; i < n; i++) {
        hash[a[i]]++;
    }

    for (let i = 0; i < n; i++) {
        if (hash[a[i]] == 1) {
            return a[i];
        }
    }
}

let arr = [1, 1, 2, 2, 3, 3, 4, 4, 5, 5, 6];
console.log(numberAppearOnes(arr, arr.length));
```

## optimal 1
## Find the Number that Appears Once (Using HashMap with Map Data Structure)

**Problem Statement:** Given a non-empty array of integers `arr`, every element appears twice except for one. Find that single one.

**Approach:**

This approach involves using a HashMap (or Map) data structure to count the occurrences of each element in the array. The algorithm iterates through the array and populates the HashMap with element counts. Finally, it searches the HashMap for the element with a count of 1, which is the single element that appears once.

- **Time Complexity:** O(N*logM) + O(M), where N is the size of the array and M is the size of the map (approximately N/2 + 1).
  - The first term, O(N*logM), is for inserting N elements into the map, where insertion takes logM time.
  - The second term, O(M), is to iterate the map and search for the single element.
- **Space Complexity:** O(M), where M is the size of the map (approximately N/2 + 1).

**Note:** The time complexity can vary depending on the map data structure used. If using an unordered_map in C++, the time complexity can be O(N) for the best and average case instead of O(N*logM).

```javascript
const numberAppearOnes = (a, n) => {
    var hashMap = new Map();

    for (let i = 0; i < n; i++) {
        var num = a[i];
        hashMap.set(num, (hashMap.get(num) || 0) + 1);
    }

    for (let [num, count] of hashMap) {
        if (count == 1) {
            return num;
        }
    }
}

let arr = [1, 1, 2, 2, 3, 3, 4, 4, 5, 5, 6];
console.log(numberAppearOnes(arr, arr.length));
```

## optimal 2
## Find the Number that Appears Once (Using XOR)

**Problem Statement:** Given a non-empty array of integers `arr`, every element appears twice except for one. Find that single one.

**Approach:**

This approach uses the XOR operation to find the number that appears only once. When you XOR two equal numbers, the result is 0, and XORing any number with 0 leaves it unchanged. By XORing all the elements in the array, the duplicates will cancel each other out, and the only remaining value will be the number that appears once.

- **Time Complexity:** O(N), where N is the size of the array.
  - The algorithm iterates through the array once to perform XOR operations.

- **Space Complexity:** O(1)
  - The algorithm uses a constant amount of extra space for variables.

```javascript
function getSingleElement(arr) {
    // XOR all the elements:
    let xorr = 0;
    for (let i = 0; i < arr.length; i++) {
        xorr = xorr ^ arr[i];
    }
    return xorr;
}

function main() {
    let arr = [4, 1, 2, 1, 2];
    let ans = getSingleElement(arr);
    console.log("The single element is:", ans);
}

main();
```


