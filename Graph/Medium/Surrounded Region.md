## Surrounded Regions

Given an m x n matrix `board` containing 'X' and 'O', capture all regions that are 4-directionally surrounded by 'X'. A region is captured by flipping all 'O's into 'X's in that surrounded region.

### Input
- `board`: An m x n matrix of characters where each cell is either 'X' or 'O'.

### Output
- Modify the `board` in-place to capture the surrounded regions.

### Constraints
- `m == board.length`
- `n == board[i].length`
- `1 <= m, n <= 200`
- `board[i][j]` is 'X' or 'O'.

### Explanation
- An 'O' should not be flipped if:
  - It is on the border, or
  - It is adjacent to an 'O' that should not be flipped.
- Example:
  - Input:
    ```plaintext
    board = [["X","X","X","X"],
             ["X","O","O","X"],
             ["X","X","O","X"],
             ["X","O","X","X"]]
    ```
  - Output:
    ```plaintext
    [["X","X","X","X"],
     ["X","X","X","X"],
     ["X","X","X","X"],
     ["X","O","X","X"]]


Explanation:
The bottom 'O' is on the border, so it is not flipped.
The other three 'O's form a surrounded region, so they are flipped.
Time Complexity
O(N) + O(M) + O(N x M x 4) ~ O(N x M)
For the worst case, every element will be marked as 'O' in the matrix, and the DFS function will be called for (N x M) nodes, and for every node, we are traversing for 4 neighbors, so it will take O(N x M x 4) time. Also, we are running loops for boundary elements, so it will take O(N) + O(M).
Space Complexity
O(N x M)
O(N x M) for the visited array, and auxiliary stack space takes up N x M locations at max.


```js
var solve = function (board) {

  const m = board.length;
  const n = board[0].length;

  const vis = new Array(m).fill(0).map(() => new Array(n).fill(0));
  const direction = [[1, 0], [-1, 0], [0, 1], [0, -1]];
  const isValid = (x, y) => { return x >= 0 && y >= 0 && x < m && y < n }

  function dfs(row, col) {
    vis[row][col] = 1;

    for (let [dx, dy] of direction) {
      let newRow = dx + row;
      let newCol = dy + col;

      //check for right, left, top col;
      if (isValid(newRow, newCol) && board[newRow][newCol] === 'O' && !vis[newRow][newCol]) {
        dfs(newRow, newCol);
      }
    }
  }

  //Traverse on boundary
  for (let j = 0; j < n; j++) {
    //Top Row
    if (!vis[0][j] && board[0][j] === 'O') {
      dfs(0, j);
    }

    //Bottom Row
    if (!vis[m - 1][j] && board[m - 1][j] === 'O') {
      dfs(m - 1, j);
    }

  }

  for (let i = 0; i < m; i++) {
    //first column
    if (!vis[i][0] && board[i][0] === 'O') {
      dfs(i, 0);
    }

    if (!vis[i][n - 1] && board[i][n - 1] === 'O') {
      dfs(i, n - 1);
    }

  }

  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      if (!vis[i][j] && board[i][j] === 'O') {
        board[i][j] = 'X';
      }
    }
  }

  return board;
}



// if not to  modify in-place
// var solve = function (board) {

//   const m = board.length;
//   const n = board[0].length;

//   const vis = new Array(m).fill('X').map(() => new Array(n).fill('X'));
//   const direction = [[1, 0], [-1, 0], [0, 1], [0, -1]];
//   const isValid = (x, y) => { return x >= 0 && y >= 0 && x < m && y < n }

//   function dfs(row, col) {
//     vis[row][col] = 'O';

//     for (let [dx, dy] of direction) {
//       let newRow = dx + row;
//       let newCol = dy + col;

//       //check for right, left, top col;
//       if (isValid(newRow, newCol) && board[newRow][newCol] === 'O' && !vis[newRow][newCol]) {
//         dfs(newRow, newCol);
//       }
//     }
//   }

//   //Traverse on boundary
//   for (let j = 0; j < n; j++) {
//     //Top Row
//     if (vis[0][j] === 'X' && board[0][j] === 'O') {
//       dfs(0, j);
//     }

//     //Bottom Row
//     if (vis[m - 1][j] === 'X' && board[m - 1][j] === 'O') {
//       dfs(m - 1, j);
//     }

//   }

//   for (let i = 0; i < m; i++) {
//     //first column
//     if (vis[i][0] === 'X' && board[i][0] === 'O') {
//       dfs(i, 0);
//     }

//     if (vis[i][n - 1] === 'X' && board[i][n - 1] === 'O') {
//       dfs(i, n - 1);
//     }

//   }

//   // for (let i = 0; i < m; i++) {
//   //   for (let j = 0; j < n; j++) {
//   //     if (!vis[i][j] && board[i][j] === 'O') {
//   //       board[i][j] = 'X';
//   //     }
//   //   }
//   // }
//   // console.log(vis)
//   return vis;
// }
```