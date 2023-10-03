## Rotten Oranges

### Problem Description

You are given an `m x n` grid where each cell can have one of three values:

- `0` representing an empty cell,
- `1` representing a fresh orange, or
- `2` representing a rotten orange.

Every minute, any fresh orange that is 4-directionally adjacent to a rotten orange becomes rotten.

Return the minimum number of minutes that must elapse until no cell has a fresh orange. If this is impossible, return -1.

### Examples

- Input: `grid = [[2, 1, 1], [1, 1, 0], [0, 1, 1]]`
  - Output: `4`

- Input: `grid = [[2, 1, 1], [0, 1, 1], [1, 0, 1]]`
  - Output: `-1`
  - Explanation: The orange in the bottom-left corner (row 2, column 0) is never rotten because rotting only happens 4-directionally.

- Input: `grid = [[0, 2]]`
  - Output: `0`
  - Explanation: Since there are already no fresh oranges at minute 0, the answer is just 0.

### Constraints

- `1 <= m, n <= 10`
- `grid[i][j]` is `0`, `1`, or `2`.
- `m == grid.length`
- `n == grid[i].length`
- `grid[i][j]` is `0`, `1`, or `2`.

### Time and Space Complexity

- **Time Complexity**: O(m * n)
- **Space Complexity**: O(m * n)

### JavaScript Code

```javascript
//Better code
/**
 * @param {number[][]} grid
 * @return {number}
 */
var orangesRotting = function (grid) {
    //get the row and column from grid to loop and find the rotten oranges i.e (2) and add those in queue initially
    //the queue with take input as [x,y,minutes];

    //Declare initial min = 0;

    //declare a fresh orange count to 0, while looping through grid,if you find any fresh orange increase the count.
    //At the end check if freshOrange count still exist, then retuen -1 or else the currentTime;

    //declare the 4 direction Traverse to visit the neighbors

    //declare isvalid fun to check the grid cell exist to that specific direction traverse.

    //while the queue.length
    //deque the first rotten oranges i.e [x,y,min]
    //consider it as min = currenMin
    //explore the neighbors using direction variable declared above. By updating the current X and y based on direction.
    //if you started exploring initially check if its valid cell and that grid is a fresh orange
    //if yes lets rotten that cell, and decrease the freshOrange Count.
    //and push this new rotten cell into queue with currentMin+1;

    //Once loop is completed means the queue is all checked,
    // check for freshOrange count it exist ans is -1, else return the min value.


    const row = grid.length;
    const col = grid[0].length;

    const directions = [[-1, 0], [1, 0], [0, 1], [0, -1]];

    let queue = [];
    let freshOrangeCount = 0;
    let min = 0;

    var isValid = (x, y) => x >= 0 && x < row && y >= 0 && y < col;

    for (let i = 0; i < row; i++) {
        for (let j = 0; j < col; j++) {
            if (grid[i][j] === 2) {
                queue.push([i, j, min]); //[x,y,min];
            } else if (grid[i][j] === 1) {
                freshOrangeCount++;
            }
        }
    }

    while (queue.length > 0) {
        const [x, y, currentMin] = queue.shift();
        min = currentMin;

        for (let [dx, dy] of directions) {
            let newX = x + dx;
            let newY = y + dy;

            if (isValid(newX, newY) && grid[newX][newY] === 1) {
                grid[newX][newY] = 2;
                freshOrangeCount--;
                queue.push([newX, newY, currentMin + 1]);
            }
        }
    }

    return freshOrangeCount === 0 ? min : -1;

};
```
```js

//normal way
/**
 * @param {number[][]} grid
 * @return {number}
 */
var orangesRotting = function (grid) {
    const qu = [];
    let noOfFreshOranges = 0;
    let time = 0;
    for (let i = 0; i < grid.length; i++) {
        for (let j = 0; j < grid[i].length; j++) {
            if (grid[i][j] === 2) qu.push([i, j]);
            if (grid[i][j] === 1) noOfFreshOranges++;
        }
    }

    while (qu.length) {
        const n = qu.length;

        let freshOrngCount = 0;
        for (let i = 0; i < n; i++) {
            const [x, y] = qu.shift();
            // right
            if ((y < grid[x].length - 1) && (grid[x][y + 1] === 1)) {
                freshOrngCount++;
                grid[x][y + 1] = 2
                qu.push([x, y + 1]);
            }
            // bottom
            if ((x < grid.length - 1) && (grid[x + 1][y] === 1)) {
                freshOrngCount++;
                grid[x + 1][y] = 2
                qu.push([x + 1, y]);
            }
            // top
            if ((x >= 1) && (grid[x - 1][y] === 1)) {
                freshOrngCount++;
                grid[x - 1][y] = 2
                qu.push([x - 1, y]);
            }
            // left
            if ((y >= 1) && (grid[x][y - 1] === 1)) {
                freshOrngCount++;
                grid[x][y - 1] = 2
                qu.push([x, y - 1]);
            }
        }
        if (freshOrngCount) time++;
        noOfFreshOranges -= freshOrngCount;
    }

    // if any fresh orange remains
    return noOfFreshOranges === 0 ? time : -1;
};
```