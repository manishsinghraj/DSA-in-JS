# Two Sum

## Problem Statement

Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.
<br>

Example 1:
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
<br>

Example 2:
Input: nums = [3,2,4], target = 6
Output: [1,2]
<br>

Example 3:
Input: nums = [3,3], target = 6
Output: [0,1]
 
<br>
Constraints:

2 <= nums.length <= 104
-109 <= nums[i] <= 109
-109 <= target <= 109
Only one valid answer exists.
 
<br>
Follow-up: Can you come up with an algorithm that is less than O(n2) time complexity?

```js
 // o(n^2)
var twoSum = function(nums, target) {
    for(let i = 0; i < nums.length; i++){
        let sum = 0;
        for(let j = i+1; j < nums.length; j++){
            sum += nums[i] + nums[j];

            if(sum === target){
                return [i, j];
            }
        }
    }
    return -1;
};
```

```js
//o(n) //o(n)
var twoSum = function(nums, target) {
    const myMap = new Map();

    for(let i = 0; i < nums.length; i++){
        let complement = target - nums[i];

        if(myMap.has(complement)){
            return [myMap.get(complement), i];
        }
        myMap.set(nums[i], i);
    }
    return -1;
}
```

```js
//o(n log n)
var twoSum = function(nums, target) {
    for (let i = 0; i < nums.length; i++) {
        const complement = target - nums[i];
        const index = binarySearch(nums, complement, i + 1);

        if (index !== -1) {
            return [i, index];
        }
    }

    return [];
}

//Binary search function
var binarySearch = function(nums, target, start) {
    let low = start;
    let high = nums.length - 1;

    while (low <= high) {
        const mid = Math.floor((low + high) / 2);

        if (nums[mid] === target) {
            return mid;
        } else if (nums[mid] < target) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }

    return -1;
}
```
### OR
```js
var twoSum = function(nums, target) {
    let indexedNum = nums.map((num, index) => ({num, index}));
     indexedNum.sort((a, b) => a.num - b.num);
    let left = 0;
    let right = nums.length - 1;

    while(left < right){
        let sum =  indexedNum[left].num + indexedNum[right].num;

        if(sum < target){
            left++
        } else if(sum > target){
            right--;
        } else{
            return [indexedNum[left].index, indexedNum[right].index];
        }
    }

    return [];
}
```
