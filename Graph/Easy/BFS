# BFS Traversal(level)

## Approach:
1. **Initial Configuration:**
    - Queue data structure: follows FIFO, and will always contain the starting node.
   - Visited array: an array initialized to 0.
    - In BFS, we start with a "starting" node, mark it as visited, and push it into the queue data structure.
   - In every iteration, we pop out the node 'v' and put it in the solution vector, as we are traversing this node.
   - All the unvisited adjacent nodes from 'v' are visited next and are pushed into the queue.The list of adjacent neighbors of the node can be accessed from the adjacency list.
   - Repeat steps 2 and 3 until the queue becomes empty, and this way you can easily traverse all the nodes in the graph.

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
