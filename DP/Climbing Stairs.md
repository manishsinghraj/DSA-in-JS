### You are climbing a staircase. It takes n steps to reach the top.Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top ?
    Example 1:

Input: n = 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
Example 2:

Input: n = 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step


Constraints:

1 <= n <= 45



## Tabulation
Time Complexity: O(N)

Reason: We are running a simple iterative loop

Space Complexity: O(N)

```js
Reason: We are using an external array of size ‘n+1’.

function climbStairs(n) {
    if (n <= 1) {
        return 1; // Base case: 0 ways for n=0, 1 way for n=1
    }

    // Create an array to store the number of ways to reach each step
    const dp = new Array(n + 1);

    // Initialize the base cases
    dp[0] = 1;
    dp[1] = 1;

    // Calculate the number of ways for each step from 2 to n
    for (let i = 2; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }

    return dp[n];
}

const n1 = 2;
console.log(climbStairs(n1)); // Output: 2

const n2 = 3;
console.log(climbStairs(n2)); // Output: 3
```


## Space optimized
Time Complexity: O(N)

Reason: We are running a simple iterative loop

Space Complexity: O(1)

Reason: We are not using any extra space.

```js
function climbStairs(n) {
    if (n <= 1) {
        return 1; // Base case: 0 ways for n=0, 1 way for n=1
    }

    let prev1 = 1;
    let prev2 = 1;
    let current = 0;

    for (let i = 2; i <= n; i++) {
        current = prev1 + prev2;
        prev1 = prev2;
        prev2 = current;
    }

    return current;
}

const n1 = 2;
console.log(climbStairs(n1)); // Output: 2

const n2 = 3;
console.log(climbStairs(n2)); // Output: 3
```