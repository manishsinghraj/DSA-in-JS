// Node class represents an element in the doubly linked list
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
