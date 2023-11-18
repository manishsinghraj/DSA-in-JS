## Reversing a Linked List

Time Complexity (TC):
The time complexity of this algorithm is O(n), where n is the number of nodes in the linked list. It iterates through the entire linked list once, visiting each node exactly once, to reverse the list.

Space Complexity (SC):
The space complexity is O(1) because the algorithm uses a constant amount of extra space regardless of the size of the linked list. It only uses a few additional pointers (prev, current, and nextNode) to perform the reversal, and the space used does not depend on the input size.

```javascript
// Definition for singly-linked list node.
function ListNode(val, next) {
    this.val = (val === undefined ? 0 : val);
    this.next = (next === undefined ? null : next);
}

// Function to reverse a linked list.
function reverseLinkedList(head) {
    if (!head || !head.next) {
        return head; // The list is empty or has only one element; no need to reverse.
    }

    let prev = null;   // Initialize a pointer to the previous node.
    let current = head; // Initialize a pointer to the current node.

    while (current !== null) {
        const nextNode = current.next; // Save the reference to the next node.
        current.next = prev;          // Reverse the pointer direction.

        // Move 'prev' and 'current' pointers one step forward.
        prev = current;
        current = nextNode;
    }

    return prev; // 'prev' now points to the new head of the reversed list.
}

const head = new ListNode(1);
head.next = new ListNode(2);
head.next.next = new ListNode(3);
head.next.next.next = new ListNode(4);
head.next.next.next.next = new ListNode(5);

console.log("Original linked list:");
let current = head;
while (current !== null) {
    console.log(current.val);
    current = current.next;
}

const reversedHead = reverseLinkedList(head);

console.log("Reversed linked list:");
current = reversedHead;
while (current !== null) {
    console.log(current.val);
    current = current.next;
}
```



# Recursion
```js
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

class LinkedList {
  constructor() {
    this.head = null;
  }

  // Function to reverse the linked list
  reverse() {
    this.head = this.reverseUtil(this.head, null);
  }

  // Helper function for reversing the linked list
  reverseUtil(current, prev) {
    // Base case: if the current node is null, the list is reversed
    if (!current) {
      return prev;
    }

    // Save the next node
    const next = current.next;

    // Reverse the link
    current.next = prev;

    // Recursively reverse the rest of the list
    return this.reverseUtil(next, current);
  }

  // Function to add a node to the beginning of the linked list
  prepend(data) {
    const newNode = new Node(data);
    newNode.next = this.head;
    this.head = newNode;
  }

  // Function to print the linked list
  print() {
    let current = this.head;
    const result = [];

    while (current) {
      result.push(current.data);
      current = current.next;
    }

    console.log(result.join(' -> '));
  }
}

// Example usage:
const linkedList = new LinkedList();
linkedList.prepend(3);
linkedList.prepend(2);
linkedList.prepend(1);

console.log("Original Linked List:");
linkedList.print();

linkedList.reverse();

console.log("Reversed Linked List:");
linkedList.print();

```
