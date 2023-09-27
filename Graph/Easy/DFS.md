## Depth-First Search (DFS) for Graph Traversal

This is an example of a Depth-First Search (DFS) algorithm for traversing a graph.

### Time Complexity

For an undirected graph: O(N) + O(2E)  
For a directed graph: O(N) + O(E)

- O(N) is the time taken for every node as we call the recursive function once.
- 2E (or E) is for the total degrees as we traverse all adjacent nodes.

### Space Complexity

O(3N) ~ O(N)

- Space is needed for the DFS stack space.
- Space is required for the `visited` array.
- Space is allocated for an adjacency list.

### JavaScript Code

```javascript
class Solution {
    // Function to return a list containing the DFS traversal of the graph.
    dfsOfGraph(V, adj) {
        const vis = new Array(V).fill(0);
        let start = 0;
        let ans = [];
        this.dfs(start, adj, vis, ans);
        return ans;
    }

    dfs(node, adj, vis, ans) {
        vis[node] = 1;
        ans.push(node);
        for (let ele of adj[node]) {
            if (!vis[ele]) {
                this.dfs(ele, adj, vis, ans);
            }
        }
    }
}
