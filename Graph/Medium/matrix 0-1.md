## Matrix 0/1

Given an m x n binary matrix `mat`, return the distance of the nearest 0 for each cell. The distance between two adjacent cells is 1.

### Constraints
- `m == mat.length`
- `n == mat[i].length`
- `1 <= m, n <= 10^4`
- `1 <= m * n <= 10^4`
- `mat[i][j]` is either 0 or 1.
- There is at least one 0 in `mat`.

### Example 1
Input: `mat = [[0,0,0],[0,1,0],[0,0,0]]`
Output: `[[0,0,0],[0,1,0],[0,0,0]]`

### Example 2
Input: `mat = [[0,0,0],[0,1,0],[1,1,1]]`
Output: `[[0,0,0],[0,1,0],[1,2,1]]`

### Time Complexity
- O(N x M + N x M x 4) ~ O(N x M)
  - For the worst case, the BFS function will be called for (N x M) nodes, and for every node, we are traversing for 4 neighbors, so it will take O(N x M x 4) time.

### Space Complexity
- O(N x M) + O(N x M) + O(N x M) ~ O(N x M)
  - O(N x M) for the visited array, distance matrix, and queue space takes up N x M locations at max.

### Note
- DFS isn't really suitable for finding the shortest path.
- DFS goes 'depth-first,' which means it finds each longest path. To identify the shortest path, you have to traverse all paths first, record their length, and then pick the shortest.
- That's why BFS is used in these cases. You try to traverse in every direction, and as soon as you hit the target point, you're done.


```js
/**
 * @param {number[][]} mat
 * @return {number[][]}
 */
var updateMatrix = function(mat) {
    const row = mat.length;
    const col = mat[0].length;
    const vis = [];
    const dis = [];
    let queue = [];
    const direction = [[0,1], [0,-1], [1,0], [-1, 0]];
    var isValid = (x, y) => x >= 0 && x < row && y >= 0 && y < col;


    for(let i = 0; i < row; i++ ){
        vis.push(new Array(col).fill(0));
        dis.push(new Array(col).fill(0));
    };


    for(let i = 0; i< row; i++){
        for(let j = 0; j < col; j++){
            if(mat[i][j] === 0){
                queue.push([i,j,0]);
                vis[i][j] = 1;
            }
        }
    }


    while(queue.length > 0){
        let [x,y,steps] = queue.shift();
        dis[x][y] = steps;

        for(let [dx,dy] of direction){
            newX = x + dx;
            newY = y + dy;

            if(isValid(newX, newY) && vis[newX][newY] === 0){
                vis[newX][newY] = 1;
                queue.push([newX, newY, steps + 1]);
            }
        }
    }
    return dis;
};

```


