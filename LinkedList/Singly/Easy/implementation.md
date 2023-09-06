```js
// Node class represents an element in the linked list
class Node {
    constructor(value) {
        this.value = value; // The data in this node
        this.next = null;  // Reference to the next node
    }
}


// LinkedList class represents the linked list itself
class LinkedList {
    constructor() {
        this.head = null; // The first node in the list
    }

    // Append a node to the end of the linked list
    append(value) {
        const newNode = new Node(value); // Create a new node
        if (!this.head) {
            this.head = newNode; // If the list is empty, make this node the head
        } else {
            let current = this.head; // Start from the head
            while (current.next) {
                current = current.next; // Traverse to the last node
            }
            current.next = newNode; // Set the last node's next to the new node
        }
    }

    // Insert a node at the beginning of the linked list
    prepend(value) {
        const newNode = new Node(value); // Create a new node
        newNode.next = this.head; // Make the new node point to the current head
        this.head = newNode; // Set the new node as the head
    }

    // Delete the first occurrence of a node with the given value
    delete(value) {
        if (!this.head) {
            return; // If the list is empty, nothing to delete
        }
        if (this.head.value === value) {
            this.head = this.head.next; // If the head has the value, update the head
            return;
        }
        let current = this.head;
        while (current.next) {
            if (current.next.value === value) {
                current.next = current.next.next; // Update the next reference to skip the node to delete
                return;
            }
            current = current.next; // Move to the next node
        }
    }

    //Search
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

    // traverse
    traverse() {
        let current = this.head;
        let result = [];
        while (current) {
            result.push(current.value);
            current = current.next;
        }

        return result.join(' -> ');
    }



    //Insert at index

    insertAtIndex(index, value) {
        if (index < 0) {
            return console.log("invalid index");
        }

        if (index === 0) {
            var newNode = new Node(value);
            newNode.next = this.head;
            this.head = newNode;
            return newNode;
        }

        var newNode = new Node(value);
        var current = this.head;
        var count = 0;

        while (current && count < index - 1) {
            current = current.next;
            count++;
        }

        if (count === index - 1 && current) {
            newNode.next = current.next;
            current.next = newNode;
            return current;
        } else {
            console.log("Index out of range");
        }
    }


    // Get at Index
    getAtIndex(index) {
        if (index < 0) {
            return console.log("invalid index");
        }
        let current = this.head;
        let currentIndex = 0;
        if (current && currentIndex === index) {
            return current;
        }

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

var myList = new LinkedList();

myList.append(100);
myList.append(200);
myList.append(300);
myList.append(400);
myList.append(500);
myList.prepend(5); // myList: 5 -> 100 -> 200 -> 300 -> 400 -> 500
myList.delete(1); // Delete the first occurrence of 1 (not in the list)
console.log(myList); // Output: LinkedList { head: Node { value: 5, next: Node { value: 100, next: [Object] } } }
console.log(myList.search(900)); // Output: null (900 not found)
console.log(myList.traverse()); // Output: "5 -> 100 -> 200 -> 300 -> 400 -> 500"
console.log(myList.insertAtIndex(0, 7)); // Insert 7 at index 0
console.log(myList.traverse()); // Output: "7 -> 5 -> 100 -> 200 -> 300 -> 400 -> 500"
console.log(myList.insertAtIndex(3, 350)); // Insert 350 at index 3
console.log(myList.traverse()); // Output: "7 -> 5 -> 100 -> 350 -> 200 -> 300 -> 400 -> 500"
console.log(myList.getAtIndex(7)); // Output: null (Index out of bound)
```