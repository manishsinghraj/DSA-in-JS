# Subarray Product Less Than K

## Given an array of integers nums and an integer k, return the number of contiguous subarrays where the product of all the elements in the subarray is strictly less than k.
<br>

Example 1:

Input: nums = [10,5,2,6], k = 100
Output: 8
Explanation: The 8 subarrays that have product less than 100 are:
[10], [5], [2], [6], [10, 5], [5, 2], [2, 6], [5, 2, 6]
Note that [10, 5, 2] is not included as the product of 100 is not strictly less than k.

<br>
Example 2:

Input: nums = [1,2,3], k = 0
Output: 0
 <br>

Constraints:

1 <= nums.length <= 3 * 104
1 <= nums[i] <= 1000
0 <= k <= 106

<br>

```js
//o(n2)
var numSubarrayProductLessThanK = function(nums, k) {
    let count = 0;
    for(let i=0;i<nums.length;i++){
        let sub = 1;
        for(let j=i;i<nums.length;j++){
            sub = sub * nums[j];
            if(sub < k) count++;
            else break;
        }
    }
    return ans;
};
```

```js
var numSubarrayProductLessThanK = function(nums, k) {
    if (k <= 1) {
        return 0;
    }

    let result = 0;
    let left = 0;
    let right = 0;
    let prod = 1;

   while(right < nums.length){
       prod = prod * nums[right];

       while(prod >= k){
           prod = prod / nums[left];
           left++;
       }

       result += right - left + 1;
       right++;
   }
    return result;
};
```
