## Number of Provinces

### Problem Description

- There are `n` cities.
- Some are connected, while some are not.
- If city `a` is directly connected to city `b`, and city `b` is directly connected to city `c`, then city `a` is indirectly connected to city `c`.
- A province is a group of directly or indirectly connected cities with no other cities outside the group.
- Given an `n x n` matrix `isConnected` where `isConnected[i][j]` is `1` if the `i`th and `j`th cities are directly connected, and `isConnected[i][j]` is `0` otherwise.
- Return the total number of provinces.

### Constraints

- `1 <= n <= 200`
- `n == isConnected.length`
- `n == isConnected[i].length`
- `isConnected[i][j]` is `1` or `0`.
- `isConnected[i][i]` is `1`.
- `isConnected[i][j]` is equal to `isConnected[j][i]`.

### Time and Space Complexity

- **Time Complexity**: O(N) + O(V + 2E)
  - O(N) for the outer loop
  - The inner loop runs a single DFS over the entire graph, and DFS takes O(V + 2E) time.
- **Space Complexity**: O(N) + O(N)
  - Space for recursion stack space and the `visited` array.

### JavaScript Code

```javascript
var findCircleNum = function (isConnected) {
    const n = isConnected.length;
    const visited = new Array(n).fill(false);
    let provinces = 0;

    const dfs = (node) => {
        visited[node] = true;
        for (let i = 0; i < n; i++) {
            if (isConnected[node][i] === 1 && !visited[i]) {
                dfs(i);
            }
        }
    };

    for (let i = 0; i < n; i++) {
        if (!visited[i]) {
            dfs(i);
            provinces++;
        }
    }

    return provinces;
};
```

### With city and neighbor var


```js
/**
 * @param {number[][]} isConnected
 * @return {number}
 */
var findCircleNum = function (isConnected) {
    const n = isConnected.length;
    const visited = new Array(n).fill(false);
    let province = 0;

    for (let city = 0; city < n; city++) {
        if (!visited[city]) {
            dfs(city);
            province++;
        }
    }

    function dfs(city) {
        visited[city] = true;
        for (let neighbor = 0; neighbor < n; neighbor++) {
            if (isConnected[city][neighbor] === 1 && !visited[neighbor]) {
                dfs(neighbor);
            }
        }
    }

    return province;
};

```
