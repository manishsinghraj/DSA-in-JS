# iterative

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

  getLengthIterative() {
    let count = 0;
    let current = this.head;

    while (current) {
      count++;
      current = current.next;
    }

    return count;
  }
}

// Example Usage:
const myList = new LinkedList();
myList.append(1);
myList.append(2);
myList.append(3);

console.log(myList.getLengthIterative()); // Output: 3

```

# Recursive

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

  getLengthRecursive(current = this.head) {
    if (!current) {
      return 0;
    }

    return 1 + this.getLengthRecursive(current.next);
  }
}

// Example Usage:
const myList = new LinkedList();
myList.append(1);
myList.append(2);
myList.append(3);

console.log(myList.getLengthRecursive()); // Output: 3

```
