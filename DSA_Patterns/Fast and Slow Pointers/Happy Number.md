# Happy Number

Write an algorithm to determine if a number n is happy.

A happy number is a number defined by the following process:

Starting with any positive integer, replace the number by the sum of the squares of its digits.
Repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1.
Those numbers for which this process ends in 1 are happy.
Return true if n is a happy number, and false if not.

 <br>

Example 1:

Input: n = 19
Output: true
Explanation:
- 12 + 92 = 82
- 82 + 22 = 68
- 62 + 82 = 100
- 12 + 02 + 02 = 1
  <br>
Example 2:

Input: n = 2
Output: false
  <br>

Constraints:

1 <= n <= 231 - 1

 <br>

```js
//Naive
var isHappy = function(n) {
    let isHappy = undefined;
    let latestN = n;

    const squaredSet = new Set();

    while(isHappy === undefined){
        let squaredNumsSum = 0;
        const squaredNums = latestN.toString().split('').map(num => num * num);

        for (let i = 0; i < squaredNums.length; i++) {
            squaredNumsSum += squaredNums[i];
        }
        
        if (squaredNumsSum == 1) {
            isHappy = true;
        }

        if (squaredSet.has(squaredNumsSum)) {
            isHappy = false;
        } else {
            squaredSet.add(squaredNumsSum);
        }

        latestN = squaredNumsSum;
    }

    return isHappy;
};

```

```js
var isHappy = function(n) {
    if(n == 1) return true; 

    let slow = n; 
    let fast = n; 

    while(true){
        slow = sumOfSquares(slow);
        fast = sumOfSquares(sumOfSquares(fast));

        if(slow == fast) break;
    }

    return slow == 1;
};

function sumOfSquares(num){
    let sum = 0;
    while(num > 0){
        let last_diget = num % 10;
        sum += last_diget**2; 
        num = Math.floor(num / 10); 
    }
    return sum;
}
```
