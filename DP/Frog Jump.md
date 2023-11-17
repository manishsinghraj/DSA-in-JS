# Frog Jump

There is a frog on the `1st` step of an `N` stairs long staircase. The frog wants to reach the `Nth` stair. `HEIGHT` is the height of the `(i+1)th` stair. If the Frog jumps from `ith` to `jth` stair, the energy lost in the jump is given by the absolute value of `(HEIGHT[i-1] - HEIGHT[j-1])`. If the Frog is on `ith` staircase, he can jump either to `(i+1)th` stair or to `(i+2)th` stair. Your task is to find the minimum total energy used by the frog to reach from `1st` stair to `Nth` stair.

## Example

If the given "HEIGHT" array is [10, 20, 30, 10], the answer is 20. The frog can jump from the 1st stair to the 2nd stair (energy lost: |20 - 10| = 10) and then jump from the 2nd stair to the last stair (energy lost: |10 - 30| = 20). So, the total energy lost is 20.


## Normal
```js 
function frogJump(ind, height) {
  if (ind === 0) return 0;

  var oneJump = frogJump(ind - 1, height) + Math.abs(height[ind] - height[ind - 1]);
  var twoJump =  Number.POSITIVE_INFINITY;

  if (ind > 1) {
    twoJump = frogJump(ind - 2, height) + Math.abs(height[ind] - height[ind - 2]);
  }

  return Math.min(oneJump, twoJump);
}
const arr = [10, 20, 30, 10];
// Example usage
console.log(frogJump(arr.length - 1, arr));
 // Output: 40
```


## Using Memo
Time Complexity: O(N)

Reason: The overlapping subproblems will return the answer in constant time O(1). Therefore the total number of new subproblems we solve is ‘n’. Hence total time complexity is O(N).

Space Complexity: O(N)

Reason: We are using a recursion stack space(O(N)) and an array (again O(N)). Therefore total space complexity will be O(N) + O(N) ≈ O(N)



```js 
function frogJump(ind, height, memo = []) {
  if (ind === 0) return 0;

  if(memo[ind]!== undefined) return memo[ind];


  var oneJump = frogJump(ind - 1, height, memo) + Math.abs(height[ind] - height[ind - 1]);
  var twoJump =  Number.POSITIVE_INFINITY;

  if (ind > 1) {
    twoJump = frogJump(ind - 2, height, memo) + Math.abs(height[ind] - height[ind - 2]);
  }

  memo[ind] = Math.min(oneJump, twoJump);
  return memo[ind];
}
const arr = [10, 20, 30, 10];
// Example usage
console.log(frogJump(arr.length - 1, arr));
 // Output: 20
```


## Using Tabulation
Time Complexity: O(N)

Reason: We are running a simple iterative loop

Space Complexity: O(N)

Reason: We are using an external array of size ‘n+1’.

```js
 function frogJumpTabulation(height) {
  const n = height.length;
  if (n === 0) return 0;

  // Create an array to store the minimum jump costs
  const dp = new Array(n);
  dp[0] = 0; // Base case: no cost to jump from the first height
  let twoJump  = Number.POSITIVE_INFINITY;
  for (let i = 1; i < n; i++) {

    let oneJump = dp[i - 1] + Math.abs(height[i] - height[i - 1]); // One jump
    if(i>1){
      twoJump =  dp[i - 2] + Math.abs(height[i] - height[i - 2]);
    }

    dp[i] = Math.min(oneJump, twoJump);
  }

  return dp[n - 1]; // The result is stored in the last element of the dp array
}

const arr = [10, 20, 30, 10];
console.log(frogJumpTabulation(arr));
```

## Space Optimised
Time Complexity: O(N)

Reason: We are running a simple iterative loop

Space Complexity: O(1)

Reason: We are not using any extra space.

```js 

function frogJumpTabulation(height) {
  const n = height.length;
  if (n === 0) return 0;

  // Create an array to store the minimum jump costs
  let prev = 0;
  let prev2 = 0;
  let current;

  let twoJump  = Number.POSITIVE_INFINITY;
  for (let i = 1; i < n; i++) {

    let oneJump = prev + Math.abs(height[i] - height[i - 1]); // One jump
    if(i>1){
      twoJump =  prev2 + Math.abs(height[i] - height[i - 2]);
    }

    current = Math.min(oneJump, twoJump);
    prev2 = prev;
    prev = current;
  }

  return prev; // The result is stored in the last element of the dp array
}

const arr = [10, 20, 30, 10];
console.log(frogJumpTabulation(arr));
```