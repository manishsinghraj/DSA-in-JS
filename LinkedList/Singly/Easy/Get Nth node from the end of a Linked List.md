```js
class Node {
  constructor(val) {
    this.val = val;
    this.next = null;
  }
}

class LinkedList {
  constructor() {
    this.head = null;
  }

  append(val) {
    const newNode = new Node(val);

    if (!this.head) {
      this.head = newNode;
    } else {
      let current = this.head;
      while (current.next) {
        current = current.next;
      }
      current.next = newNode;
    }
  }

  nthNodeFromEnd(n) {
    if (n <= 0) {
      console.log("Invalid value of N");
      return null;
    }

    let fast = this.head;
    let slow = this.head;

    // Move fast pointer N nodes ahead
    for (let i = 0; i < n; i++) {
      if (fast === null) {
        console.log("N is greater than the length of the list");
        return null;
      }
      fast = fast.next;
    }

    // Move both pointers until fast reaches the end
    while (fast !== null) {
      fast = fast.next;
      slow = slow.next;
    }

    return slow;
  }

  print() {
    let current = this.head;
    let result = [];
    while (current) {
      result.push(current.val);
      current = current.next;
    }
    console.log(result.join(" -> "));
  }
}

// Example Usage:
const myList = new LinkedList();
myList.append(1);
myList.append(2);
myList.append(3);
myList.append(4);

console.log("Original Linked List:");
myList.print();

const nthNodeFromEnd = myList.nthNodeFromEnd(2); // Getting the 2nd node from the end
if (nthNodeFromEnd) {
  console.log("Nth Node from the end:", nthNodeFromEnd.val);
}

```
