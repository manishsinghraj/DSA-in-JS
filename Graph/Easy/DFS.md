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



## Using Stack

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


```js
dfs(V, adj) {
    const vis = new Array(V).fill(false);
    let stack = [];
    let ans = [];
    const start = 0;
    stack.push(start);

    while (stack.length > 0) {
        const node = stack.pop();

        if (!vis[node]) {
            vis[node] = true;
            ans.push(node);
        }

        for (let neighbor of adj[node]) {
            if (!vis[neighbor]) {
                stack.push(neighbor);
            }
        }
    }
    return ans;
}
```

# Transitive Closure of a Graph using DFS

```js
class Graph {
  constructor(vertices) {
    this.vertices = vertices;
    this.adjacencyMatrix = Array.from({ length: vertices }, () => Array(vertices).fill(0));
  }

  addEdge(from, to) {
    this.adjacencyMatrix[from][to] = 1;
  }

  transitiveClosure() {
    const closure = Array.from({ length: this.vertices }, () => Array(this.vertices).fill(false));

    for (let i = 0; i < this.vertices; i++) {
      this.dfs(i, i, closure);
    }

    return closure;
  }

  dfs(start, current, closure) {
    closure[start][current] = true;
    // console.log(`${[start]}, ${[current]} - ${closure[start][current]}`)
    for (let next = 0; next < this.vertices; next++) {
      // console.log(`${[current]}, ${[next]} -  ${this.adjacencyMatrix[current][next]}`)
      if (this.adjacencyMatrix[current][next] && !closure[start][next]) {
        this.dfs(start, next, closure);
      }
    }
  }
}

// Example usage:
const graph = new Graph(4);

graph.addEdge(0, 1);
graph.addEdge(0, 2);
graph.addEdge(1, 2);
graph.addEdge(2, 0);
graph.addEdge(2, 3);
graph.addEdge(3, 3);



for(let row of graph.adjacencyMatrix){
  console.log(row)
}

const closureMatrix = graph.transitiveClosure();

console.log("Transitive Closure Matrix:");
for (let row of closureMatrix) {
  console.log(row);
}

// graph:
// [0, 1, 1, 0]
// [0, 0, 1, 0]
// [1, 0, 0, 1]
// [0, 0, 0, 1]

// Transitive Closure Matrix:
// [true, true, true, true]
// [true, true, true, true]
// [true, true, true, true]
// [false, false, false, true]

```
