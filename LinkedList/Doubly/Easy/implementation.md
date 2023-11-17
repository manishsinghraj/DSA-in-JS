##  Node class represents an element in the doubly linked list

```js
class Node {
    constructor(value) {
        this.value = value; // The data in this node
        this.prev = null;  // Reference to the previous node
        this.next = null;  // Reference to the next node
    }
}

// DoublyLinkedList class represents the doubly linked list itself
class DoublyLinkedList {
    constructor() {
        this.head = null; // The first node in the list
    }

    // Append a node to the end of the doubly linked list
    append(value) {
        const newNode = new Node(value); // Create a new node
        if (!this.head) {
            this.head = newNode; // If the list is empty, make this node the head
        } else {
            let current = this.head; // Start from the head
            while (current.next) {
                current = current.next; // Traverse to the last node
            }
            newNode.prev = current; // Set the new node's prev to the last node
            current.next = newNode; // Set the last node's next to the new node
        }
    }

    // Insert a node at the beginning of the doubly linked list
    prepend(value) {
        const newNode = new Node(value); // Create a new node
        newNode.next = this.head; // Make the new node point to the current head
        if (this.head) {
            this.head.prev = newNode; // If the list is not empty, update the head's prev
        }
        this.head = newNode; // Set the new node as the head
    }

    // Delete the first occurrence of a node with the given value
    delete(value) {
        if (!this.head) {
            return; // If the list is empty, nothing to delete
        }
        if (this.head.value === value) {
            this.head = this.head.next; // If the head has the value, update the head
            if (this.head) {
                this.head.prev = null; // If the list is not empty, update the new head's prev
            }
            return;
        }
        let current = this.head;
        while (current.next) {
            if (current.next.value === value) {
                current.next = current.next.next; // Update the next reference to skip the node to delete
                if (current.next) {
                    current.next.prev = current; // If the node to delete is not the last, update the next node's prev
                }
                return;
            }
            current = current.next; // Move to the next node
        }
    }

    // Search
    search(value) {
        let current = this.head;
        while (current) {
            if (current.value === value) {
                return current;
            }
            current = current.next;
        }
        return null;
    }

    // Traverse
    traverse() {
        let current = this.head;
        let result = [];
        while (current) {
            result.push(current.value);
            current = current.next;
        }
        return result.join(' <-> ');
    }

    // Insert at Index
    insertAtIndex(index, value) {
        if (index < 0) {
            return console.log("Invalid index");
        }

        if (index === 0) {
            const newNode = new Node(value);
            newNode.next = this.head;
            if (this.head) {
                this.head.prev = newNode;
            }
            this.head = newNode;
            return newNode;
        }

        const newNode = new Node(value);
        let current = this.head;
        let count = 0;

        while (current && count < index - 1) {
            current = current.next;
            count++;
        }

        if (count === index - 1 && current) {
            newNode.prev = current;
            newNode.next = current.next;
            if (current.next) {
                current.next.prev = newNode;
            }
            current.next = newNode;
            return current;
        } else {
            console.log("Index out of range");
        }
    }

    // Get at Index
    getAtIndex(index) {
        if (index < 0) {
            return console.log("Invalid index");
        }

        let current = this.head;
        let currentIndex = 0;

        while (current && currentIndex < index) {
            current = current.next;
            currentIndex++;
        }

        if (currentIndex === index && current) {
            return current;
        } else {
            console.log("Index out of bound");
            return null;
        }
    }
}

// Example usage
var myDoublyList = new DoublyLinkedList();

myDoublyList.append(100);
myDoublyList.append(200);
myDoublyList.append(300);
myDoublyList.append(400);
myDoublyList.append(500);
myDoublyList.prepend(5); // myDoublyList: 5 <-> 100 <-> 200 <-> 300 <-> 400 <-> 500
myDoublyList.delete(1); // Delete the first occurrence of 1 (not in the list)
console.log(myDoublyList); // Output: DoublyLinkedList { head: Node { value: 5,
```


# Doubly Circular Linked List


```js
// Node class represents an element in the circular doubly linked list
class Node {
    constructor(value) {
        this.value = value; // The data in this node
        this.prev = null;  // Reference to the previous node
        this.next = null;  // Reference to the next node
    }
}

// CircularDoublyLinkedList class represents the circular doubly linked list itself
class CircularDoublyLinkedList {
    constructor() {
        this.head = null; // The first node in the list
    }

    // Append a node to the end of the circular doubly linked list
    append(value) {
        const newNode = new Node(value); // Create a new node
        if (!this.head) {
            this.head = newNode; // If the list is empty, make this node the head
            newNode.next = this.head; // Make the new node point to itself
            newNode.prev = this.head; // Set the new node's prev to the head
        } else {
            let current = this.head; // Start from the head
            while (current.next !== this.head) {
                current = current.next; // Traverse to the last node
            }
            newNode.prev = current; // Set the new node's prev to the last node
            current.next = newNode; // Set the last node's next to the new node
            newNode.next = this.head; // Make the new node point to the head
            this.head.prev = newNode; // Update the head's prev to the new node
        }
    }

    // Insert a node at the beginning of the circular doubly linked list
    prepend(value) {
        const newNode = new Node(value); // Create a new node
        if (!this.head) {
            this.head = newNode; // If the list is empty, make this node the head
            newNode.next = this.head; // Make the new node point to itself
            newNode.prev = this.head; // Set the new node's prev to the head
        } else {
            newNode.next = this.head; // Make the new node point to the current head
            newNode.prev = this.head.prev; // Set the new node's prev to the last node
            this.head.prev.next = newNode; // Update the next reference of the last node
            this.head.prev = newNode; // Update the head's prev to the new node
            this.head = newNode; // Set the new node as the head
        }
    }

    // Delete the first occurrence of a node with the given value
    delete(value) {
        if (!this.head) {
            return; // If the list is empty, nothing to delete
        }
        let current = this.head;
        do {
            if (current.value === value) {
                if (current.next === this.head) {
                    // If the node to delete is the last node, update the next reference of the previous node
                    current.prev.next = this.head;
                    this.head.prev = current.prev;
                } else if (current === this.head) {
                    // If the node to delete is the head, update the next reference of the previous last node
                    current.prev.next = current.next;
                    current.next.prev = current.prev;
                    this.head = current.next;
                } else {
                    // If the node to delete is in the middle, update the next reference of the previous and next nodes
                    current.prev.next = current.next;
                    current.next.prev = current.prev;
                }
                return;
            }
            current = current.next; // Move to the next node
        } while (current !== this.head); // Continue until we reach the head again
    }

    // Search
    search(value) {
        if (!this.head) {
            return null; // If the list is empty, the value cannot be found
        }
        let current = this.head;
        do {
            if (current.value === value) {
                return current;
            }
            current = current.next; // Move to the next node
        } while (current !== this.head); // Continue until we reach the head again
        return null;
    }

    // Traverse
    traverse() {
        if (!this.head) {
            return ''; // If the list is empty, return an empty string
        }
        let current = this.head;
        let result = '';
        do {
            result += current.value + ' <-> ';
            current = current.next; // Move to the next node
        } while (current !== this.head); // Continue until we reach the head again
        return result.slice(0, -5); // Remove the trailing ' <-> ' from the result
    }

    // Insert at Index
    insertAtIndex(index, value) {
        if (index < 0) {
            return console.log("Invalid index");
        }

        const newNode = new Node(value);

        if (index === 0) {
            if (!this.head) {
                // If the list is empty, make this node the head
                this.head = newNode;
                newNode.next = this.head;
                newNode.prev = this.head;
            } else {
                // If the list is not empty, insert at the beginning
                newNode.next = this.head;
                newNode.prev = this.head.prev;
                this.head.prev.next = newNode;
                this.head.prev = newNode;
                this.head = newNode;
            }
            return newNode;
        }

        let current = this.head;
        let count = 0;

        do {
            if (count === index - 1) {
                newNode.prev = current;
                newNode.next = current.next;
                current.next.prev = newNode;
                current.next = newNode;
                return current;
            }
            current = current.next;
            count++;
        } while (current !== this.head);

        console.log("Index out of range");
    }

    // Get at Index
    getAtIndex(index) {
        if (index < 0) {
            return console.log("Invalid index");
        }

        let current = this.head;
        let currentIndex = 0;

        do {
            if (currentIndex === index) {
                return current;
            }
            current = current.next;
            currentIndex++;
        } while (current !== this.head);

        console.log("Index out of bound");
        return null;
    }
}

// Example usage
var myCircularDoublyList = new CircularDoublyLinkedList();

myCircularDoublyList.append(100);
myCircularDoublyList.append(200);
myCircularDoublyList.append(300);
myCircularDoublyList.append(400);
myCircularDoublyList.append(500);
myCircularDoublyList.prepend(5); // myCircularDoublyList: 5 <-> 500 <-> 400 <-> 300 <-> 200 <-> 100
myCircularDoublyList.delete(200); // Delete the first occurrence of 200
console.log(myCircularDoublyList); // Output: CircularDoublyLinkedList { head: Node { value: 5, ... } }
console.log(myCircularDoublyList.search(300)); // Output: Node { value: 300, ... }
console.log(myCircularDoublyList.traverse()); // Output: "5 <-> 500 <-> 400 <-> 300 <-> 100"
console.log(myCircularDoublyList.insertAtIndex(2, 350)); // Insert 350 at index 2
console.log(myCircularDoublyList.traverse()); // Output: "5 <-> 500 <-> 350 <-> 400 <-> 300 <-> 100"
console.log(myCircularDoublyList.getAtIndex(4)); // Output: Node { value: 300, ... }


```
