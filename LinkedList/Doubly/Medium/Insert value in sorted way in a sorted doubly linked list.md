```js
class Node {
  constructor(data) {
    this.data = data;
    this.prev = null;
    this.next = null;
  }
}

const insertIntoSortedDLL = (head, value) => {
  const newNode = new Node(value);

  // Case 1: Empty DLL
  if (!head) {
    return newNode;
  }

  // Case 2: Insert at the beginning
  if (value <= head.data) {
    newNode.next = head;
    head.prev = newNode;
    return newNode;
  }

  let current = head;

  // Case 3: Insert in the middle or at the end
  while (current.next) {
    if (current.next.data > value) {
      newNode.prev = current;
      newNode.next = current.next;
      current.next.prev = newNode;
      current.next = newNode;
      return head;
    }
    current = current.next;
  }

  // Case 4: Insert at the end
  newNode.prev = current;
  current.next = newNode;

  return head;
};

```
