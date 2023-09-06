What is a linked list, and how does it differ from an array?
Example: A linked list is a linear data structure where each element is a separate object called a node. These nodes are linked together to form a sequence. In contrast, an array is a contiguous block of memory that stores elements of the same type.

Answer: Linked lists are flexible in size and allow for dynamic memory allocation, making them suitable for scenarios like managing a playlist in a music player, where you may frequently add or remove songs without a fixed size.

What are the different types of linked lists?
Example: There are different types of linked lists, such as singly linked lists, doubly linked lists, and circular linked lists.

Answer: A singly linked list is used in scenarios like maintaining a to-do list, while a doubly linked list is useful for tasks like implementing a web browser's backward and forward navigation history.

How do you implement a basic singly linked list in your preferred programming language?
Example: Implement a singly linked list in Python.

Answer: See code examples for creating, inserting, deleting, and traversing a singly linked list.

Explain the concept of a doubly linked list and its advantages over a singly linked list.
Example: In a text editor, a doubly linked list can be used for implementing an "Undo" and "Redo" functionality, allowing users to navigate backward and forward through editing changes.

Answer: A doubly linked list has "previous" and "next" pointers, enabling bidirectional traversal and making it efficient for tasks that require both backward and forward navigation.

What is a circular linked list, and when might you use it?
Example: In a round-robin scheduling algorithm used in operating systems, a circular linked list is employed to maintain a queue of processes that take turns executing.

Answer: Circular linked lists are suitable for scenarios where elements need to be processed cyclically or when you want to create a looping data structure.

How do you find the middle node of a linked list?
Example: In a social media application, finding the middle user in a list of followers can be done by finding the middle node of a linked list representing the follower list.

Answer: There are various algorithms for finding the middle node of a linked list, such as using two pointers (slow and fast pointers) or calculating the length of the list.

How do you detect if a linked list has a cycle (loop)?
Example: In GPS navigation systems, detecting cycles in road networks can help identify traffic congestion. Linked list cycle detection is used to prevent navigation loops.

Answer: Algorithms like Floyd's Tortoise and Hare are used to detect cycles in linked lists. It's crucial for tasks where you want to avoid infinite loops.

What is a self-adjusting linked list, and how does it work?
Example: In web browsers, a self-adjusting linked list can be used to cache frequently visited web pages for faster navigation. The most frequently accessed pages move to the front of the list.

Answer: Self-adjusting linked lists reorganize elements based on access frequency to optimize access times, making them suitable for scenarios where frequently accessed items need to be readily available.

Compare and contrast arrays and linked lists in terms of time complexity for various operations.
Example: In a database management system, understanding the time complexity of data retrieval using arrays and linked lists helps optimize query processing.

Answer: Arrays have constant-time access but slower insertions and deletions, while linked lists have slower access but faster insertions and deletions.

What are the applications of linked lists in real-world scenarios or programming problems?
Example: In a computer-based inventory system, linked lists can be used to manage product lists that change frequently, with items being added or removed.

Answer: Linked lists are valuable in scenarios where the size of the data structure needs to adjust dynamically, such as maintaining a shopping cart on an e-commerce website.

These real-world examples provide context for understanding the significance of linked lists and how they are applied in various domains and scenarios.




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
