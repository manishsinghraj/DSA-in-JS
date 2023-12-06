The stock span problem is a financial problem where we have a series of N daily price quotes for a stock and we need to calculate the span of the stock’s price for all N days. The span Si of the stock’s price on a given day i is defined as the maximum number of consecutive days just before the given day, for which the price of the stock on the current day is less than or equal to its price on the given day. 

Examples:

Input: N = 7, price[] = [100 80 60 70 60 75 85]
Output: 1 1 1 2 1 4 6
Explanation: Traversing the given input span for 100 will be 1, 80 is smaller than 100 so the span is 1, 60 is smaller than 80 so the span is 1, 70 is greater than 60 so the span is 2 and so on. Hence the output will be 1 1 1 2 1 4 6.

Input: N = 6, price[] = [10 4 5 90 120 80]
Output:1 1 2 4 5 1
Explanation: Traversing the given input span for 10 will be 1, 4 is smaller than 10 so the span will be 1, 5 is greater than 4 so the span will be 2 and so on. Hence, the output will be 1 1 2 4 5 1.


- Input: N = 7, price[] = [100 80 60 70 60 75 85]
- Output: 1 1 1 2 1 4 6


## Naive Sol
O(n^2), O(n)

```js
const stackSpan = (prices) => {
  const n = prices.length;
  const span = new Array(n).fill(0);
  span[0] = 1;

  for (let i = 1; i < n; i++) {
    span[i] = 1;
    for (let j = i - 1; j >= 0; j--) {
      if (prices[j] <= prices[i]) {
        span[i]++;
      } else {
        break; // Break out of the inner loop when the condition is not met
      }
    }
  }
  return span;
}

// Example usage:
const stockPrices = ["100", "80", "60", "70", "60", "75", "85"].map(Number);
const spanResult = stackSpan(stockPrices);

console.log("Stock Prices:", stockPrices);
console.log("Stock Spans:", spanResult);

OR


const stackSpan = (prices) => {
  const n = prices.length;
  const span = new Array(n).fill(0);
  span[0] = 1;

  for (let i = 1; i < n; i++) {
    span[i] = 1;
    for (let j = i - 1; j >= 0 && prices[j] <= prices[i]; j--) {
      span[i]++;
    }
  }
  return span;
}

// Example usage:
const stockPrices = ["100", "80", "60", "70", "60", "75", "85"].map(Number);
const spanResult = stackSpan(stockPrices);

console.log("Stock Prices:", stockPrices);
console.log("Stock Spans:", spanResult);

```



Better using Stack

```js
const stackSpan = (prices) => {
  const n = prices.length;
  const span = new Array(n).fill(0);
  const stack = [];

  for (let i = 0; i < n; i++) {
    while (stack.length > 0 && prices[stack[stack.length - 1]] <= prices[i]) {
      stack.pop();
    } 
      span[i] = stack.length === 0 ? i + 1 : i - stack[stack.length - 1];
      stack.push(i);
  }

  return span;


}



// Example usage:
const stockPrices = ["100", "80", "60", "70", "60", "75", "85"].map(Number);
const spanResult = stackSpan(stockPrices);

console.log("Stock Prices:", stockPrices);
console.log("Stock Spans:", spanResult);

```
