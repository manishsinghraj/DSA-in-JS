# Course Schedule I - Topological Sorting

You are given a total of `numCourses` courses labeled from 0 to `numCourses - 1`. You are also given an array `prerequisites`, where each element `[ai, bi]` indicates that you must take course `bi` first if you want to take course `ai`. The goal is to determine if it's possible to finish all courses. If possible, return `true`; otherwise, return `false`.

**Example 1:**

Input: `numCourses = 2`, `prerequisites = [[1, 0]]`
Output: `true`
Explanation: There are 2 courses to take. To take course 1, you should have finished course 0. So it is possible.

**Example 2:**

Input: `numCourses = 2`, `prerequisites = [[1, 0], [0, 1]]`
Output: `false`
Explanation: There are 2 courses to take. To take course 1, you should have finished course 0, and to take course 0, you should also have finished course 1. So it is impossible.

**Constraints:**
- 1 <= `numCourses` <= 2000
- 0 <= `prerequisites.length` <= 5000
- `prerequisites[i].length` == 2
- 0 <= `ai`, `bi` < `numCourses`
- All the pairs `prerequisites[i]` are unique.

## Code Explanation

```javascript
function canFinish(numCourses, prerequisites) {
  // Create an adjacency list to represent the course dependencies
  const graph = new Array(numCourses).fill(0).map(() => []);
  for (const [course, prerequisite] of prerequisites) {
    graph[course].push(prerequisite);
  }

  // Step 1: Initialize in-degrees and a queue for nodes with no incoming edges
  const inDegrees = new Array(numCourses).fill(0);
  const queue = [];

  // Calculate in-degrees for each node
  for (let i = 0; i < numCourses; i++) {
    for (const neighbor of graph[i]) {
      inDegrees[neighbor]++;
    }
  }

  // Step 2: Find nodes with no incoming edges and add them to the queue
  for (let i = 0; i < numCourses; i++) {
    if (inDegrees[i] === 0) {
      queue.push(i);
    }
  }

  // Step 3: Initialize the result list
  const result = [];

  // Step 4: Process nodes with no incoming edges
  while (queue.length > 0) {
    const node = queue.shift(); // Dequeue a node
    result.push(node); // Add it to the result

    // Update in-degrees of neighboring nodes and enqueue those with no incoming edges
    for (const neighbor of graph[node]) {
      inDegrees[neighbor]--;
      if (inDegrees[neighbor] === 0) {
        queue.push(neighbor);
      }
    }
  }

    // // Step 5: Check for cycles (if there are nodes left in the result)
  // if (result.length !== numCourses) {
  //   console.error("The graph contains a cycle. Topological sorting is not possible.");
  //   return [];
  // }

  // Step 5: Check for cycles (if there are nodes left in the result)
  if (result.length !== numCourses) {
    return false;
  }

  return true;
}

// Example usage:
const numCourses = 5;
const prerequisites = [[0, 1], [0, 2], [1, 3], [1, 4], [3, 4]];

console.log(canFinish(numCourses, prerequisites)); // Output: false (there's a cycle)
```