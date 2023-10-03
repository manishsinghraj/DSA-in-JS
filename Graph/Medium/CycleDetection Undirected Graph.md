# Cycle detection in undirected graph

## Time Complexity
- O(N + 2E) + O(N), where N = Nodes, 2E is for total degrees as we traverse all adjacent nodes. In the case of connected components of a graph, it will take another O(N) time.

## Space Complexity
- O(N) + O(N) ~ O(N), Space for the queue data structure and the visited array.

```javascript
class Solution {
  detect(src, adj, vis) {
    vis[src] = 1;
    const queue = [];
    queue.push([src, -1]);

    while (!queue.length === 0) {
      const [node, parent] = queue.shift();

      for (const adjacentNode of adj[node]) {
        if (!vis[adjacentNode]) {
          vis[adjacentNode] = 1;
          queue.push([adjacentNode, node]);
        } else if (parent !== adjacentNode) {
          return true;
        }
      }
    }

    return false;
  }

  isCycle(V, adj) {
    const vis = new Array(V).fill(0);
    for (let i = 0; i < V; i++) {
      if (!vis[i]) {
        if (this.detect(i, adj, vis)) return true;
      }
    }
    return false;
  }
}

const adj = [[], [2], [1, 3], [2]];
const obj = new Solution();
const ans = obj.isCycle(4, adj);
if (ans) {
  console.log("1");
} else {
  console.log("0");
}
