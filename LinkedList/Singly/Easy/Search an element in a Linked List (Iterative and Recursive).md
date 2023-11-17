# Iterative

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

  searchIterative(target) {
    let current = this.head;
    while (current) {
      if (current.val === target) {
        return true; // Element found
      }
      current = current.next;
    }
    return false; // Element not found
  }
}

// Example Usage:
const myList = new LinkedList();
myList.append(1);
myList.append(2);
myList.append(3);

console.log(myList.searchIterative(2)); // Output: true
console.log(myList.searchIterative(4)); // Output: false

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

  searchRecursive(target, current = this.head) {
    if (!current) {
      return false; // Element not found
    }

    if (current.val === target) {
      return true; // Element found
    }

    return this.searchRecursive(target, current.next);
  }
}

// Example Usage:
const myList = new LinkedList();
myList.append(1);
myList.append(2);
myList.append(3);

console.log(myList.searchRecursive(2)); // Output: true
console.log(myList.searchRecursive(4)); // Output: false

```
