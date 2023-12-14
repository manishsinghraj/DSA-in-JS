# BFS Traversal(level)

## Approach:
1. **Initial Configuration:**
    - Queue data structure: follows FIFO, and will always contain the starting node.
   - Visited array: an array initialized to 0.
    - In BFS, we start with a "starting" node, mark it as visited, and push it into the queue data structure.
   - In every iteration, we pop out the node 'v' and put it in the solution vector, as we are traversing this node.
   - All the unvisited adjacent nodes from 'v' are visited next and are pushed into the queue.The list of adjacent neighbors of the node can be accessed from the adjacency list.
   - Repeat steps 2 and 3 until the queue becomes empty, and this way you can easily traverse all the nodes in the graph.
     
  
    Step 1: Define a Queue of size total number of vertices in the 
            graph. 

    Step 2: Select any vertex as the starting point for traversal. 
            Visit that vertex and insert it into the Queue.  

    Step 3: Visit all the adjacent vertices of the vertex, that is 
             in front of the Queue and is not visited, and insert 
             them into the Queue. 

    Step 4: When there is no new vertex to visit from the vertex in 
            front of the Queue, delete that vertex from the 
            Queue.  

    Step 5: Repeat steps 3 and 4 until the queue becomes empty.  

    Step 6: When the queue becomes Empty, produce the final 
            spanning-tree by removing unused edges from the graph.
   

Time Complexity: O(N) + O(2E), Where N = Nodes, 2E is for total degrees as we traverse all adjacent nodes.

Space Complexity: O(3N) ~ O(N), Space for queue data structure visited array and an adjacency list

```javascript
class Solution {
    bfsOfGraph(V, adj) {
        const vis = new Array(V).fill(0);
        vis[0] = 1;
        const q = [];
        q.push(0);
        const bfs = [];

        while (q.length > 0) {
            const node = q.shift();
            bfs.push(node);

            for (const neighbor of adj[node]) {
                if (!vis[neighbor]) {
                    vis[neighbor] = 1;
                    q.push(neighbor);
                }
            }
        }

        return bfs;
    }
}

function addEdge(adj, u, v) {
    adj[u].push(v);
    adj[v].push(u);
}

function printAns(ans) {
    for (let i = 0; i < ans.length; i++) {
        console.log(ans[i] + " ");
    }
}

const adj = Array(6).fill().map(() => []);
addEdge(adj, 0, 1);
addEdge(adj, 1, 2);
addEdge(adj, 1, 3);
addEdge(adj, 0, 4);

const obj = new Solution();
const ans = obj.bfsOfGraph(5, adj);
printAns(ans);
```

# BFS for Disconnected Graph

```js
class Graph {
    constructor() {
        this.adjacencyList = {};
    }

    addVertex(vertex) {
        if (!this.adjacencyList[vertex]) {
            this.adjacencyList[vertex] = [];
        }
    }

    addEdge(vertex1, vertex2) {
        this.adjacencyList[vertex1].push(vertex2);
        this.adjacencyList[vertex2].push(vertex1);
    }

    bfs(startingVertex) {
        const queue = [startingVertex];
        const visited = {};
        const result = [];

        visited[startingVertex] = true;

        while (queue.length > 0) {
            const currentVertex = queue.shift();
            result.push(currentVertex);

            this.adjacencyList[currentVertex].forEach(neighbor => {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.push(neighbor);
                }
            });
        }

        // Check for remaining vertices not visited in case of a disconnected graph
        for (let vertex in this.adjacencyList) {
            if (!visited[vertex]) {
                visited[vertex] = true;
                result.push(vertex);

                // Continue BFS for the remaining connected components
                queue.push(vertex);

                while (queue.length > 0) {
                    const currentVertex = queue.shift();
                    this.adjacencyList[currentVertex].forEach(neighbor => {
                        if (!visited[neighbor]) {
                            visited[neighbor] = true;
                            queue.push(neighbor);
                        }
                    });
                }
            }
        }

        return result;
    }
}

// Example usage:
const graph = new Graph();

graph.addVertex('A');
graph.addVertex('B');
graph.addVertex('C');
graph.addVertex('D');
graph.addVertex('E');

graph.addEdge('A', 'B');
graph.addEdge('A', 'C');
graph.addEdge('D', 'E');

console.log("BFS for Disconnected Graph:", graph.bfs('A'));

```
