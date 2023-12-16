# Cycle Detection in Directed Graph

### Time Complexity (TC):

The time complexity is primarily influenced by the depth-first search (DFS) traversal of the graph.

1. **DFS:**
   - The DFS algorithm has a time complexity of O(V + E), where V is the number of vertices and E is the number of edges.
   - In the worst case, the algorithm may visit all vertices and edges in the graph.

2. **Loop Over Vertices:**
   - There is a loop that iterates over each vertex in the graph.
   - Each DFS call takes O(V + E) time.

Therefore, the overall time complexity is O(V^2 + VE), where V is the number of vertices and E is the number of edges in the graph.

### Space Complexity (SC):

The space complexity is determined by the auxiliary space used during the DFS traversal and the space required for storing the graph.

1. **DFS Stack (Recursion Stack):**
   - The space required for the recursion stack during DFS is O(V).
   - This is because, in the worst case, the recursion stack may contain all vertices.

2. **Visited and PathVis Arrays:**
   - Two arrays (`vis` and `pathVis`) of size V are used to keep track of visited nodes.
   - The space complexity for these arrays is O(V).

3. **Adjacency List:**
   - The adjacency list representation of the graph requires O(V + E) space, where V is the number of vertices and E is the number of edges.

Therefore, the overall space complexity is O(V + E).

In summary:
- **Time Complexity:** O(V^2 + VE)
- **Space Complexity:** O(V + E)

```javascript
const detectCycleInDirectedGraph = (V, adj) => {
    const dfsCheck = (src, adj, vis, pathVis) => {
        vis[src] = 1;
        pathVis[src] = 1;

        // Traversal of adj nodes
        for (let node of adj[src]) {
            if (!vis[node]) {
                if (dfsCheck(node, adj, vis, pathVis)) return true;
            } else if (pathVis[node]) {
                return true;
            }
        }

        pathVis[src] = 0;
        return false;
    };

    const isCycle = (V, adj) => {
        const vis = new Array(V).fill(0);
        const pathVis = new Array(V).fill(0);

        for (let i = 0; i < V; i++) {
            if (!vis[i]) {
                if (dfsCheck(i, adj, vis, pathVis)) return true;
            }
        }
        return false;
    };

    return isCycle(V, adj);
};

// Example usage:
const vertices = 4;
const adjacencyList = {
    0: [1],
    1: [2],
    2: [0],
    3: [2],
};

const hasCycle = detectCycleInDirectedGraph(vertices, adjacencyList);
console.log("Does the directed graph have a cycle?", hasCycle);
```

