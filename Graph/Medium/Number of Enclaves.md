## Number of Enclaves

You are given an `m x n` binary matrix `grid`, where `0` represents a sea cell and `1` represents a land cell.

A move consists of walking from one land cell to another adjacent (4-directionally) land cell or walking off the boundary of the grid.

Return the number of land cells in `grid` for which we cannot walk off the boundary of the grid in any number of moves.

### Example 1

**Input:**

```
grid = [[0,0,0,0],
        [1,0,1,0],
        [0,1,1,0],
        [0,0,0,0]]

Output: 3
Explanation: There are three 1s that are enclosed by 0s, and one 1 that is not enclosed because its on the boundary.
```
```
Input: grid = [[0,1,1,0],[0,0,1,0],[0,0,1,0],[0,0,0,0]]
Output: 0
Explanation: All 1s are either on the boundary or can reach the boundary.
```

```js
/**
 * @param {number[][]} grid
 * @return {number}
 */
var numEnclaves = function (grid) {
  const m = grid.length;
  const n = grid[0].length;
  const vis = new Array(m).fill(0).map(() => new Array(n).fill(0));
  let queue = [];
  const direction = [[1, 0], [-1, 0], [0, -1], [0, 1]];
  const isValid = (x, y) => { return x >= 0 && y >= 0 && x < m && y < n };
  let count = 0;

  //Traverse though Boundary and get lands and insert to the queue.
  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      if ((i === 0 || j === 0 || i === m - 1 || j === n - 1) && grid[i][j] === 1) {
          queue.push([i, j]);
          vis[i][j] = 1;
      }
    }
  }


  while (queue.length > 0) {
    const [x, y] = queue.shift();

    for (let [dx, dy] of direction) {
      const newX = dx + x;
      const newY = dy + y;

      if (isValid(newX, newY) && !vis[newX][newY] && grid[newX][newY] === 1) {
        vis[newX][newY] = 1;
        queue.push([newX, newY]);
      }
    }
  }

  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      if (grid[i][j] === 1 && !vis[i][j]) {
        count++;
      }
    }
  }
  return count;
};

```