# Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

## Notice that the solution set must not contain duplicate triplets.

 
<br>
Example 1:

Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation: 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.

<br>
Example 2:

Input: nums = [0,1,1]
Output: []
Explanation: The only possible triplet does not sum up to 0.

<br>
Example 3:

Input: nums = [0,0,0]
Output: [[0,0,0]]
Explanation: The only possible triplet sums up to 0.

<br>
 

Constraints:

3 <= nums.length <= 3000
-105 <= nums[i] <= 105

<br>

```js
// o(n^3) //o(m)
var threeSum = function(nums) {
    let n = nums.length;
    let st = new Set();
    let ans = []

    // check all possible triplets:
    for (let i = 0; i < n; i++) {
        for (let j = i + 1; j < n; j++) {
            for (let k = j + 1; k < n; k++) {
                if (nums[i] + nums[j] + nums[k] === 0) {
                    let temp = [nums[i], nums[j], nums[k]];
                    temp.sort((a, b) => a - b);
                    ans.push(temp);
                }
            }
        }
    }

    //store the set in the answer:
    let set  = new Set(ans.map(JSON.stringify));
    ans = Array.from(set).map(JSON.parse);
    return ans;

};

```

```js
//o(n^2) //o(m)
var threeSum = function(nums) {
    let n = nums.length;
    let ans = [];

    for(let i = 0; i < n; i++){
        let set = new Set();
        for(let j = i + 1; j < n; j++){
            let k = -(nums[i] + nums[j]);

            if(set.has(k)){
                let temp = [k, nums[i], nums[j]];
                temp.sort((a,b) => a - b);
                ans.push(temp);
            } else {
                set.add(nums[j]);
            }

        }

    }

    set = new Set(ans.map(JSON.stringify));
    ans = Array.from(set).map(JSON.parse);
    return ans;
};

```

```js
- Time Complexity: O(NlogN)+O(N2), where N = size of the array.
- Reason: The pointer i, is running for approximately N times. And both the pointers j and k combined can run for approximately N times including the operation of skipping duplicates. So the total time complexity will be O(N2).

- Space Complexity: O(no. of quadruplets), This space is only used to store the answer. We are not using any extra space to solve this problem. So, from that perspective, space complexity can be written as O(1).

var threeSum = function(nums) {
    let n = nums.length;
    let ans = [];
    nums.sort((a,b) => a- b);

    for(let i = 0; i < n; i++){

        if(i!==0 && nums[i] === nums[i-1]) continue;

        let j = i+1;
        let k = n - 1;

        while(j < k){
            let sum = nums[i] + nums[j] + nums[k];

            if(sum === 0){
                ans.push([nums[i] ,  nums[j] , nums[k]]);
                j++;
                k--;

                while(j < k && nums[j] === nums[j-1]){j++};
                while(j < k && nums[k] === nums[k+1]){k--};

            }else if(sum < 0){
                j++;
            }else {
                k--;
            }
        }
    }
    return ans;
};
```
