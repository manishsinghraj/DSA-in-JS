## Depth-First Search (DFS) for Graph Traversal


    Step 1: Define a Stack of size total number of vertices in the 
            graph.

    Step 2: Select any vertex as the starting point for traversal. 
            Visit that vertex and push it on to the Stack.

    Step 3: Visit any one of the adjacent vertices of the vertex,
            that is at top of the stack and is not visited, and 
            push it on to the stack. 

    Step 4: Repeat step 3 until there are no new vertices to visit 
            from each vertex on top of the stack.  

    Step 5: When there is no new vertex to visit, use 
            backtracking and pop one vertex from the stack. 

    Step 6: Repeat steps 3, 4, and 5 until stack becomes Empty.  

    Step 7: When stack becomes Empty, produce the final 
            spanning-tree by removing unused edges from the graph.


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
