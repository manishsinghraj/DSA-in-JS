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