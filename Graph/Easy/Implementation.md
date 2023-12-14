# Adjacency List
```js
class Graph {
    constructor() {
        this.adjacencyList = {};
    }

    //ADD Node
    addVerterx(vertex) {
        if (!this.adjacencyList[vertex]) {
            this.adjacencyList[vertex] = new Set();
        }
    }

    //ADD Edge
    addEdge(vertex1, vertex2) {
        if (!this.adjacencyList[vertex1]) {
            this.addVerterx(vertex1);
        }
        if (!this.adjacencyList[vertex2]) {
            this.addVerterx(vertex2);
        }
        this.adjacencyList[vertex1].add(vertex2);
        this.adjacencyList[vertex2].add(vertex1); //undirected Graph
    }

    //CHECK for Edge
    hasEdge(vertex1, vertex2) {
        if (!this.adjacencyList[vertex1] || !this.adjacencyList[vertex2]) return false;
        return this.adjacencyList[vertex1].has(vertex2) && this.adjacencyList[vertex2].has(vertex1);
    }

    //REMOVE the Edge
    removeEdge(vertex1, vertex2) {
        if (this.hasEdge(vertex1, vertex2)) {
            this.adjacencyList[vertex1].delete(vertex2);
            this.adjacencyList[vertex2].delete(vertex1);
        } else {
            return "No edge found";
        }
    }


    //REMOVE the Vertex
    removeVertex(vertex) {
        if (!this.adjacencyList[vertex]) {
            return console.log("vertex not found");
        }

        for (let adjacentVertex of this.adjacencyList[vertex]) {
            this.removeEdge(vertex, adjacentVertex);
        }

        delete this.adjacencyList[vertex];
    }



    //PRINT the Graph
    display() {
        for (let vertex in this.adjacencyList) {
            console.log(vertex + " -> " + [...this.adjacencyList[vertex]]);
        }
    }

    //OR

    // display() {
    //     for (let [vertex, neighbors] of Object.entries(this.adjacencyList)) {
    //         console.log(`${vertex} -> ${[...neighbors]}`);
    //     }
    // }
}


var graph = new Graph();
graph.addVertex('A');
graph.addVertex('B');
graph.addVertex('C');

graph.addEdge('A', 'B');
graph.addEdge('B', 'C');

console.log("Graph after adding vertices A, B, and C, and edges A-B and B-C:");
graph.display();

console.log("Does the graph have an edge between A and B?", graph.hasEdge("A", 'B')); // true
console.log("Does the graph have an edge between D and C?", graph.hasEdge("D", 'C')); // false

console.log("====================");

console.log("Attempting to remove vertex 'E' (which doesn't exist):");
graph.removeVertex('E'); // Vertex not found
console.log("Removing vertex 'B':");
graph.removeVertex('B'); // Removes vertex 'B' and its incident edges
console.log("Graph after removing vertex 'B' and its incident edges:");
graph.display();

console.log("Does the graph have an edge between A and B?", graph.hasEdge("A", 'B')); // false
console.log("Does the graph have an edge between A and C?", graph.hasEdge("A", 'C')); // true

console.log("Attempting to remove edge 'B-A':");
graph.removeEdge('B', 'A'); // No edge found

console.log("Graph after attempting to remove edge 'B-A':");
graph.display();
```

```
Graph after adding vertices A, B, and C, and edges A-B and B-C:
A -> B
B -> A,C
C -> B
Does the graph have an edge between A and B? true
Does the graph have an edge between D and C? false
====================
Attempting to remove vertex 'E' (which doesn't exist):
vertex not found
Removing vertex 'B':
Graph after removing vertex 'B' and its incident edges:
A ->
C ->
Does the graph have an edge between A and B? false
Does the graph have an edge between A and C? false
Attempting to remove edge 'B-A':
Graph after attempting to remove edge 'B-A':
A ->
C ->
```


# Adjacency Matrix

```JS
class Graph {
  constructor() {
    this.vertices = [];
    this.adjacencyMatrix = [];
  }

  // addVertex
  addVertex(vertex) {
    if (!this.vertices.includes(vertex)) {
      this.vertices.push(vertex);

      // Extend the adjacency matrix for the new vertex
      for (let row of this.adjacencyMatrix) {
        row.push(0);
      }
      console.log("this.adjacencyMatrix1", this.adjacencyMatrix); //when 2 vertices are added, this is how it looks - [ [ 0, 0 ] ]

      const newRow = new Array(this.vertices.length).fill(0);
      this.adjacencyMatrix.push(newRow);
      console.log("this.adjacencyMatrix2", this.adjacencyMatrix); //when 2 vertices are added, this is how it looks - [ [ 0, 0 ], [ 0, 0 ] ]
    }
  }

  // addEdge
  addEdge(vertex1, vertex2) {
    const index1 = this.vertices.indexOf(vertex1);
    const index2 = this.vertices.indexOf(vertex2);

    if (index1 === -1 || index2 === -1) {
      console.log("Vertices not found");
      return;
    }

    this.adjacencyMatrix[index1][index2] = 1;
    this.adjacencyMatrix[index2][index1] = 1;
  }

  // hasEdge
  hasEdge(vertex1, vertex2) {
    const index1 = this.vertices.indexOf(vertex1);
    const index2 = this.vertices.indexOf(vertex2);

    if (index1 === -1 || index2 === -1) {
      console.log("Vertices not found");
      return false;
    }

    return this.adjacencyMatrix[index1][index2] === 1 && this.adjacencyMatrix[index2][index1] === 1;
  }

  // removeEdge
  removeEdge(vertex1, vertex2) {
    const index1 = this.vertices.indexOf(vertex1);
    const index2 = this.vertices.indexOf(vertex2);

    if (index1 === -1 || index2 === -1) {
      console.log("Vertices not found");
      return;
    }

    this.adjacencyMatrix[index1][index2] = 0;
    this.adjacencyMatrix[index2][index1] = 0;
  }

  // removeVertex
  removeVertex(vertex) {
    const index = this.vertices.indexOf(vertex);

    if (index === -1) {
      console.log("Vertex not found");
      return;
    }

    // Remove the vertex from vertices array
    this.vertices.splice(index, 1);

    // Remove the corresponding row and column from the adjacency matrix
    this.adjacencyMatrix.splice(index, 1);
    for (let row of this.adjacencyMatrix) {
      row.splice(index, 1);
    }
  }

  // Display
  display() {
    console.log("Vertices:", this.vertices);
    console.log("Adjacency Matrix:");

    for (let row of this.adjacencyMatrix) {
      console.log(row);
    }
  }
}

// Example usage:
const graph = new Graph();

graph.addVertex('A');
graph.addVertex('B');
graph.addVertex('C');
graph.addVertex('D');

graph.addEdge('A', 'B');
graph.addEdge('A', 'C');
graph.addEdge('B', 'D');

graph.display();


//output

// this.adjacencyMatrix1[]
// this.adjacencyMatrix2[[0]]
// this.adjacencyMatrix1[[0, 0]]
// this.adjacencyMatrix2[[0, 0], [0, 0]]
// this.adjacencyMatrix1[[0, 0, 0], [0, 0, 0]]
// this.adjacencyMatrix2[[0, 0, 0], [0, 0, 0], [0, 0, 0]]
// this.adjacencyMatrix1[[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]]
// this.adjacencyMatrix2[[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]]


// Vertices: ['A', 'B', 'C', 'D']


// Adjacency Matrix:
// [0, 1, 1, 0]
// [1, 0, 0, 1]
// [1, 0, 0, 0]
// [0, 1, 0, 0]

```
