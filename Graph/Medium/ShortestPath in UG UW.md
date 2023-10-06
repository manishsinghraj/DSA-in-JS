# Finding Shortest Path in an Undirected Unweighted Graph

## Time Complexity (TC)

- Building the adjacency list: O(E), where E is the number of edges.
- The Breadth-First Search (BFS) traversal: O(V + E), where V is the number of vertices and E is the number of edges. In the worst case, BFS may visit all vertices and edges.
- Overall, the time complexity of the `findShortestPath` function is dominated by the BFS traversal, so it's O(V + E), where V is the number of vertices and E is the number of edges in the graph.

## Space Complexity (SC)

- The space complexity is primarily determined by the data structures used:
  - `adjacentList` (adjacency list): O(V + E), as it stores the graph structure.
  - `vis` (visited array): O(V), where V is the number of vertices.
  - `parent` (parent dictionary): O(V), where V is the number of vertices.
  - `queue` (queue for BFS): O(V), where V is the number of vertices.
  - `ans` (result path): O(V), where V is the number of vertices.
- Overall, the space complexity of the `findShortestPath` function is O(V + E), where V is the number of vertices and E is the number of edges in the graph.

```javascript
function findShortestPath(src, dest, edges) {
  // Create an adjacency list using a JavaScript object
  const adjacentList = {};

  for (const [vertex1, vertex2] of edges) {
    if (!adjacentList[vertex1]) {
      adjacentList[vertex1] = new Set();
    }
    if (!adjacentList[vertex2]) {
      adjacentList[vertex2] = new Set();
    }
    adjacentList[vertex1].add(vertex2);
    adjacentList[vertex2].add(vertex1); // For an undirected graph
  }

  const vis = {};
  const parent = {};
  const queue = [];
  queue.push(src);
  vis[src] = true;

  // BFS
  while (queue.length > 0) {
    const node = queue.shift();

    for (const neighbor of adjacentList[node]) {
      if (!vis[neighbor]) {
        vis[neighbor] = true;
        parent[neighbor] = node;
        queue.push(neighbor);
      }
    }
  }

  // Get the shortest path
  const ans = [];
  ans.push(dest);
  let currentNode = dest;

  while (currentNode !== src) {
    currentNode = parent[currentNode];
    ans.push(currentNode);
  }

  return ans.reverse();
}

// Example usage:
const edges = [
  [1, 2],
  [1, 3],
  [2, 4],
  [2, 5],
  [3, 6],
  [4, 7],
  [5, 8],
  [6, 9],
  [7, 8],
  [8, 9]
];

const shortestPath = findShortestPath(1, 9, edges);
console.log(shortestPath); // Output: [1, 2, 4, 7, 8, 9]
```