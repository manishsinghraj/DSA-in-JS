# Finding Shortest Distances for Each Node in an Undirected `Unit Weighted` Graph

The given JavaScript function `findShortestDist` finds the shortest distance from a source node `src` to all other nodes in an undirected weighted graph using Breadth-First Search (BFS). The distances are stored in an array called `distances`. If a node is not reachable from the source node, its distance will remain as `-1` in the `distances` array.

## Code Explanation

```javascript
function findShortestDist(src, edges) {
  // Create an adjacency list
  const adjacentList = {};

  for (const [vertex1, vertex2] of edges) {
    if (!adjacentList[vertex1]) adjacentList[vertex1] = new Set();
    if (!adjacentList[vertex2]) adjacentList[vertex2] = new Set();

    adjacentList[vertex1].add(vertex2);
    adjacentList[vertex2].add(vertex1); // For an undirected graph
  }

  // Initialize an array to store distances
  const distances = new Array(edges.length).fill(-1);

  // BFS
  const queue = [];
  queue.push([src, 0]); // [node, distance]
  distances[src] = 0;

  while (queue.length > 0) {
    const [node, distance] = queue.shift();

    for (const neighbor of adjacentList[node]) {
      if (distances[neighbor] === -1) { // Check if not visited
        distances[neighbor] = distance + 1;
        queue.push([neighbor, distance + 1]); // Corrected bracket
      }
    }
  }

  return distances;
}

// Example usage:
const edges = [
  [0, 1],
  [0, 3],
  [3, 4],
  [4, 5],
  [5, 6],
  [1, 2],
  [2, 6],
  [6, 7],
  [7, 8],
  [6, 8]
];

const shortestDistances = findShortestDist(0, edges);
console.log(shortestDistances);
