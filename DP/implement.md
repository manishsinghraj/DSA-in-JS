## Normal Recursion
Time Complexity (TC):

The time complexity of this recursive Fibonacci function is exponential, specifically O(2^n). This is because, for each recursive call, the function makes two additional recursive calls until it reaches the base cases. As a result, the number of function calls grows exponentially with the input n.

Space Complexity (SC):

The space complexity of this recursive function is O(n) in the worst case. This is due to the space required for the call stack. In the worst case, there will be n function calls on the call stack, and each call consumes some space for its arguments and local variables. The space used on the call stack is proportional to the input value n.

```js
function fibonacciRecursive(n) {
    if (n <= 1) {
        return n;
    }
    return fibonacciRecursive(n - 1) + fibonacciRecursive(n - 2);
}

// Example usage
console.log(fibonacciRecursive(10)); // Output: 55
```

## Using Memo 1

Time Complexity: O(N)

Reason: The overlapping subproblems will return the answer in constant time O(1). Therefore the total number of new subproblems we solve is ‘n’. Hence total time complexity is O(N).

Space Complexity: O(N)

Reason: We are using a recursion stack space(O(N)) and an array (again O(N)). Therefore total space complexity will be O(N) + O(N) ≈ O(N)

```js
function fibonacciDP(n, memo = []) {
    if (n <= 1) {
        return n;
    }
    if (memo[n]) {
        return memo[n];
    }

    memo[n] = fibonacciDP(n - 1, memo) + fibonacciDP(n - 2, memo);
    return memo[n];
}

// Example usage
console.log(fibonacciDP(10)); // Output: 55

```

## Using Memo 2
```js 
function fibonacci(n, dp) {
    if (n <= 1) {
        return n;
    }

    if (dp[n] !== -1) {
        return dp[n];
    }

    dp[n] = fibonacci(n - 1, dp) + fibonacci(n - 2, dp);
    return dp[n];
}

const n = 5;
const dp = Array(n + 1).fill(-1);
console.log(fibonacci(n, dp)); // Output: 5
```

## Using Tabulation
Time Complexity: O(N)

Reason: We are running a simple iterative loop

Space Complexity: O(N)

Reason: We are using an external array of size ‘n+1’.

```js 
function fibonacciTabulation(n) {
    if (n <= 1) {
        return n;
    }

    const fib = new Array(n + 1);
    fib[0] = 0;
    fib[1] = 1;

    for (let i = 2; i <= n; i++) {
        fib[i] = fib[i - 1] + fib[i - 2];
    }

    return fib[n];
}

const n = 5;
console.log(fibonacciTabulation(n)); // Output: 5
```

## Using Tabulation Space Optimised
Time Complexity: O(N)

Reason: We are running a simple iterative loop

Space Complexity: O(1)

Reason: We are not using any extra space
```js
function fibonacciTabulationOptimized(n) {
    if (n <= 1) {
        return n;
    }

    let prev1 = 0;
    let prev2 = 1;

    for (let i = 2; i <= n; i++) {
        const current = prev1 + prev2;
        prev1 = prev2;
        prev2 = current;
    }

    return prev2;
}

const n = 5;
console.log(fibonacciTabulationOptimized(n)); // Output: 5
```


---
# Dynamic Programming Problem Solving

## Step 1: Identify a DP Problem
1. Identify the problem that can be solved using dynamic programming.

## Step 2: To Solve the Problem After Identification
1. Try to represent the given problem in terms of an index.
2. Perform all possible operations on that index according to the problem statement.
3. To count all possible ways, sum all the results.
   To find the minimum/maximum, take the minimum/maximum of all the results.

## Memoization (Top-Down)
1. Define a recursive function to break down the problem into smaller subproblems.
2. Cache/store results of subproblems to avoid redundant calculations.

## Tabulation (Bottom-Up)
1. Create an array to store results for all possible subproblems.
2. Fill the array using loops, starting from the base cases and working up to the final problem.

## Memoization (Top-Down)
1. Define a function to solve the problem recursively, breaking it down into smaller subproblems.
2. Create a data structure (usually an array or dictionary) to cache/store the results of subproblems.
3. Before solving a subproblem, check if the result is already cached. If it is, return the cached result.
4. If the result is not cached, solve the subproblem recursively and store the result in the cache.
5. Continue solving subproblems, using the cache to avoid redundant calculations.
6. Return the result for the original problem.

## Tabulation (Bottom-Up)
1. Understand the problem and identify the recursive nature of the problem. Determine how smaller subproblems can be used to solve larger problems.
2. Create an array (or a multi-dimensional array) to store the results for all possible subproblems.
3. Initialize the base cases in the array (usually the simplest cases that don't require further calculation).
4. Use loops to fill in the array, starting from the base cases and working up to the final problem you want to solve.
5. Calculate the result for each subproblem based on the results of smaller subproblems, following the problem's recurrence relation.
6. Continue filling the array until you reach the final problem, and the result will be stored in the array.
7. Return the result for the original problem, which is usually found at a specific location in the array.
