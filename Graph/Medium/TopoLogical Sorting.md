# Topological Sorting

Topological sorting is a concept in graph theory that helps you arrange the nodes (vertices) of a directed graph in a linear order such that for every directed edge (a, b), node 'a' comes before node 'b' in the order. This order is useful in various applications, like scheduling tasks with dependencies or finding a sequence of courses to take in a curriculum.

## Important Points and Rules

### Directed Acyclic Graph (DAG)

Topological sorting is only applicable to directed graphs that do not have any cycles. Cycles make it impossible to define a linear order because you'd have situations where a node depends on itself indirectly through a cycle.

### Nodes Represent Tasks

In many cases, nodes in a topological sort represent tasks, jobs, or events, and directed edges indicate dependencies. If task 'A' depends on task 'B', there is a directed edge from 'B' to 'A.'

### Start with Nodes that Have No Dependencies

To perform topological sorting, start with nodes that have no incoming edges. These are tasks that don't depend on any other tasks and can be done first. Add them to the sorted order.

### Remove Processed Nodes

After adding a node to the sorted order, remove it and its outgoing edges from the graph. This step represents completing the task and its dependencies.

### Repeat Until Done

Continue this process, selecting nodes with no incoming edges, adding them to the sorted order, and removing them until you've sorted all nodes. If you reach a point where no node has zero incoming edges, and the graph isn't empty, it means there's a cycle, and topological sorting is not possible.

### Multiple Valid Orders

It's important to note that there can be multiple valid topological orders for a graph, especially if there are nodes that have no dependencies and can be done concurrently.

In summary, topological sorting is a way to order tasks or nodes in a directed acyclic graph based on their dependencies. You start with nodes that have no dependencies, remove them from the graph, and repeat the process until you've ordered all the nodes. It's a crucial algorithm in various fields where managing dependencies is essential.


# Topological Sorting and Its Real-World Applications

Topological sorting is a concept in graph theory used to arrange the nodes (vertices) of a directed graph in a linear order, ensuring that for every directed edge (a, b), node 'a' comes before node 'b' in the order. This concept is valuable in various applications, such as scheduling tasks with dependencies or determining the order of events in a curriculum.

## Understanding Dependencies

In the context of topological sorting, a node having no dependencies means there are no incoming directed edges (inward arrows) pointing to that node. In a directed acyclic graph (DAG), each directed edge represents a dependency relationship between nodes. A node without incoming edges implies that no other tasks or nodes depend on it, allowing it to be executed first.

## Real-World Example: Building a House

Let's illustrate topological sorting with a real-world example: building a house. Here are some tasks involved, along with their dependencies:

- Excavation (No dependencies)
- Foundation (Depends on Excavation)
- Framing (Depends on Foundation)
- Roofing (Depends on Framing)
- Plumbing and Wiring (Depends on Framing)
- Drywall (Depends on Plumbing and Wiring)
- Painting (Depends on Drywall)
- Flooring (Depends on Painting)
- Exterior Work (Depends on Framing)
- Final Inspection (Depends on all previous tasks)

Performing topological sorting on this graph yields the following sequence of tasks:

1. Excavation
2. Foundation
3. Framing
4. Roofing
5. Plumbing and Wiring
6. Exterior Work (can happen concurrently with tasks 3 and 5)
7. Drywall
8. Painting
9. Flooring
10. Final Inspection

This sequence ensures that each task is completed after its dependencies have been fulfilled, essential for the successful construction of the house.

## Real-World Applications

Topological sorting has various practical applications in different fields:

1. **Task Scheduling:** Used in project management or job scheduling to manage tasks with dependencies and meet deadlines.
2. **Compiler Design:** Helps compilers determine the order to compile code statements or functions while resolving dependencies correctly.
3. **Build Systems:** Build tools like Make and CMake use it to compile software projects efficiently, considering source file dependencies.
4. **Course Scheduling:** Universities employ it to create course schedules, ensuring prerequisites are taken before advanced courses.
5. **Dependency Resolution:** Package managers (e.g., npm for Node.js) use it to resolve and install dependencies in the correct order.
6. **Data Flow Analysis:** Useful in determining the order of data flow through various parts of a program.
7. **Network Routing:** Routers in computer networking use it to find the optimal path for data packets.
8. **Recommendation Systems:** Recommender systems apply it to present recommendations in the right order based on user preferences and dependencies.
9. **Dependency Management:** In software projects, including version control systems like Git, it resolves dependencies and merges code changes correctly.
10. **Workflow Management:** Workflow automation tools use it to design and execute workflows with each step depending on the successful completion of previous steps.

These examples highlight the critical role of topological sorting in ensuring tasks or elements are processed in the correct order while respecting their dependencies.

## Interview Questions

In interviews, questions related to topological sorting may assess your understanding of the concept, problem-solving skills, and ability to apply it in real-world scenarios. Here are some interview questions you might encounter:



# Interview Questions on Topological Sorting

## What is Topological Sorting, and When Is It Used?

Topological sorting is a concept in graph theory used to arrange the nodes (vertices) of a directed graph in a linear order, ensuring that for every directed edge (a, b), node 'a' comes before node 'b' in the order. It is used in various applications such as scheduling tasks with dependencies, compiling code, and managing project timelines.

## Explain the Concept of a Directed Acyclic Graph (DAG). Why Is It Essential for Topological Sorting?

A Directed Acyclic Graph (DAG) is a directed graph that does not contain any cycles. Cycles are loops where you can follow directed edges and return to the same node. In topological sorting, a DAG is essential because cycles make it impossible to define a linear order due to circular dependencies.

## Can You Describe a Real-World Scenario Where Topological Sorting Would Be Useful?

Consider a project management scenario where tasks have dependencies. Topological sorting can help determine the order in which tasks should be executed to meet deadlines and ensure that dependent tasks are completed before dependent ones.

## Walk Me Through the Algorithm for Performing Topological Sorting on a Graph.

To perform topological sorting:
1. Start with nodes having no incoming edges (tasks with no dependencies).
2. Add them to the sorted order and remove them along with their outgoing edges.
3. Repeat this process until all nodes are ordered. If no node has zero incoming edges but the graph isn't empty, there's a cycle.

## What Is the Significance of Nodes with No Incoming Edges in Topological Sorting?

Nodes with no incoming edges represent tasks or nodes that don't depend on any other tasks and can be executed first. They are the starting points for topological sorting and anchor the sorting process.

## How Do You Detect Cycles in a Graph When Attempting to Perform Topological Sorting?

To detect cycles while performing topological sorting, use techniques like Depth-First Search (DFS) or Kahn's algorithm. If at any point during the sorting, you encounter a node that has not been processed but has incoming edges, it indicates a cycle in the graph.

## In a Given Directed Graph, Can There Be More Than One Valid Topological Sorting Order? If So, Provide an Example.

Yes, there can be multiple valid topological sorting orders, especially if nodes have no dependencies and can be executed concurrently. For example, in a simple linear graph, the order of nodes can be reversed while still respecting dependencies.

## Discuss the Time Complexity of the Algorithm You Would Use for Topological Sorting.

The time complexity of topological sorting depends on the algorithm used. Kahn's algorithm has a time complexity of O(V + E), where V is the number of vertices (nodes) and E is the number of edges in the graph. Other algorithms like Depth-First Search (DFS) can also be used with similar time complexities.

## Explain How Topological Sorting Can Be Applied in Software Development or Project Management.

In software development and project management, topological sorting is used to manage tasks with dependencies. It ensures tasks are executed in the right order, such as compiling code, resolving dependencies, or scheduling project tasks to meet deadlines.

## In a Practical Coding Scenario, How Would You Implement Topological Sorting? Can You Provide a Code Example in Your Preferred Programming Language?


## What are some common applications or tools that utilize topological sorting algorithms?

## How does topological sorting differ from other sorting algorithms, such as bubble sort or quicksort?

## These questions can vary in complexity, so it's a good idea to be prepared to answer both basic and more advanced questions about topological sorting, its applications, and its implementation. Practice and a strong understanding of the underlying concepts will help you excel in such interviews.


```js
// Time Complexity: O(V+E)+O(V), where V = no. of nodes and E = no. of edges. There can be at most V components. So, another O(V) time complexity.

// Space Complexity: O(2N) + O(N) ~ O(2N): O(2N) for the visited array and the stack carried during DFS calls and O(N) for recursive stack space, where N = no. of nodes.


class Solution {
  constructor() {
    this.vis = [];
    this.stack = [];
  }

  dfs(node, adj) {
    this.vis[node] = 1;
    for (let i = 0; i < adj[node].length; i++) {
      const neighbor = adj[node][i];
      if (!this.vis[neighbor]) {
        this.dfs(neighbor, adj);
      }
    }
    this.stack.push(node);
  }

  topoSort(V, adj) {
    this.vis = new Array(V).fill(0);
    this.stack = [];

    for (let i = 0; i < V; i++) {
      if (!this.vis[i]) {
        this.dfs(i, adj);
      }
    }

    return this.stack.reverse();
  }
}

// Example usage
const adj = [[], [], [3], [1], [0, 1], [0, 2]];
const V = 6;
const obj = new Solution();
const ans = obj.topoSort(V, adj);

console.log(ans.join(" ")); // Print the topological order

```



# Kahn's Algorithm for Topological Sorting

Kahn's algorithm for topological sorting serves a specific purpose in efficiently finding a topological order of nodes in a directed acyclic graph (DAG). While it's true that you can solve the problem of topological sorting by other methods, Kahn's algorithm offers several advantages:

## Efficiency

Kahn's algorithm has a time complexity of O(V + E), where V is the number of nodes (vertices) and E is the number of edges in the graph. This linear time complexity makes it one of the most efficient algorithms for topological sorting, especially for large graphs.

## Simplicity

Kahn's algorithm is relatively simple to understand and implement. It doesn't require recursive function calls or complex data structures, making it accessible for a wide range of applications.

## Guaranteed Correctness

If the algorithm successfully produces a topological order, it guarantees that the input graph is a directed acyclic graph (DAG). This property can be useful for verifying the acyclic nature of a graph, which is essential in many scenarios.

## Detecting Cycles

If the graph is not a DAG (i.e., it contains cycles), Kahn's algorithm can detect this condition. Detecting cycles can be valuable for error-checking and handling cyclic dependencies, ensuring the integrity of the topological order.

## Parallel Processing

The algorithm's structure lends itself to parallel processing or multithreading, as nodes with no incoming edges can be processed concurrently. This parallelization potential can significantly speed up the sorting process for large graphs.

## Space Efficiency

Kahn's algorithm uses minimal additional data structures, such as queues, to track nodes with no incoming edges. This minimal memory footprint makes it space-efficient and suitable for memory-constrained environments.

## Incremental Processing

In cases where you need to find a partial topological order or incrementally build a topological order as new tasks or dependencies are introduced, Kahn's algorithm can be adapted for such scenarios. Its incremental nature allows for flexibility in various applications.

While it's possible to devise other algorithms for topological sorting, Kahn's algorithm stands out for its efficiency and simplicity. It's a go-to choice when you want to find a topological order in a directed acyclic graph, and it can be applied to a wide range of real-world problems, including scheduling tasks, building software, and optimizing resource allocation.


```js
Time Complexity: O(V+E), where V = no. of nodes and E = no. of edges. This is a simple BFS algorithm.

Space Complexity: O(N) + O(N) ~ O(2N), O(N) for the indegree array, and O(N) for the queue data structure used in BFS(where N = no.of nodes).


function topologicalSort(V, adj) {
  // Step 1: Initialize in-degrees and a queue for nodes with no incoming edges
  const inDegrees = new Array(V).fill(0);
  const queue = [];

  // Calculate in-degrees for each node
  for (let i = 0; i < V; i++) {
    for (const neighbor of adj[i]) {
      inDegrees[neighbor]++;
    }
  }

  // Step 2: Find nodes with no incoming edges and add them to the queue
  for (let i = 0; i < V; i++) {
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
    for (const neighbor of adj[node]) {
      inDegrees[neighbor]--;
      if (inDegrees[neighbor] === 0) {
        queue.push(neighbor);
      }
    }
  }

  // Step 5: Check for cycles (if there are nodes left in the result)
  if (result.length !== V) {
    console.error("The graph contains a cycle. Topological sorting is not possible.");
    return [];
  }

  return result; // Return the topological order
}

// Example usage:
const V = 6;
const adj = [[], [], [3], [1], [0, 1], [0, 2]];
const topologicalOrder = topologicalSort(V, adj);
console.log(topologicalOrder); // Output: [4, 5, 0, 2, 1, 3]
```