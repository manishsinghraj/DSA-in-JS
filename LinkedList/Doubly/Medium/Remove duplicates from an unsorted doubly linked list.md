```js
class Node {
  constructor(data) {
    this.data = data;
    this.prev = null;
    this.next = null;
  }
}

const removeDuplicatesFromUnsortedDLL = (head) => {
  if (!head) {
    return null;
  }

  const seenValues = new Set();
  let current = head;

  while (current) {
    if (seenValues.has(current.data)) {
      // Duplicate found, remove the node
      current.prev.next = current.next;
      if (current.next) {
        current.next.prev = current.prev;
      }
    } else {
      // First occurrence of the value, add to the set
      seenValues.add(current.data);
    }

    current = current.next;
  }

  return head;
};

// Example usage:
// Create an unsorted doubly linked list: 3 <-> 6 <-> 2 <-> 6 <-> 3
const node1 = new Node(3);
const node2 = new Node(6);
const node3 = new Node(2);
const node4 = new Node(6);
const node5 = new Node(3);

node1.next = node2;
node2.prev = node1;
node2.next = node3;
node3.prev = node2;
node3.next = node4;
node4.prev = node3;
node4.next = node5;
node5.prev = node4;

const head = removeDuplicatesFromUnsortedDLL(node1);

// Print the modified list
let current = head;
while (current) {
  console.log(current.data);
  current = current.next;
}

```
