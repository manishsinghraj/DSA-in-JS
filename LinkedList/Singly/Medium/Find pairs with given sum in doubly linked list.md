# Brute Force

```js
class Node {
  constructor(data) {
    this.data = data;
    this.prev = null;
    this.next = null;
  }
}

class DoublyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  append(data) {
    const newNode = new Node(data);
    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      newNode.prev = this.tail;
      this.tail.next = newNode;
      this.tail = newNode;
    }
  }

  findPairsWithSum(sum) {
    let pairs = [];

    if (!this.head || !this.head.next) {
      return pairs;
    }

    let first = this.head;

    while (first) {
      let second = first.next;

      while (second) {
        if (first.data + second.data === sum) {
          pairs.push([first.data, second.data]);
        }

        second = second.next;
      }

      first = first.next;
    }

    return pairs;
  }
}

// Example Usage:
const doublyList = new DoublyLinkedList();
doublyList.append(1);
doublyList.append(2);
doublyList.append(3);
doublyList.append(4);
doublyList.append(5);

const sumToFind = 7;
const resultPairs = doublyList.findPairsWithSum(sumToFind);

console.log(`Pairs with sum ${sumToFind}: `, resultPairs);

```


# Better

```js
const findPairsInDLL = (head, target) => {
  const seenValues = new Set();
  const pairs = [];

  let current = head;

  while (current) {
    const difference = target - current.val;

    if (seenValues.has(difference)) {
      pairs.push([current.val, difference]);
    }

    seenValues.add(current.val);
    current = current.next;
  }

  return pairs;
};

```


# Optimal

```js
class Node {
  constructor(val) {
    this.val = val;
    this.prev = null;
    this.next = null;
  }
}

const findPairsInDLL = (head, x) => {
  let pairs = [];
  let start = head;
  let end = findEnd(head);

  while (start !== null && end !== null && start !== end && start.next !== end) {
    let sum = start.val + end.val;

    if (sum === x) {
      pairs.push([start.val, end.val]);
      start = start.next;
      end = end.prev;
    } else if (sum < x) {
      start = start.next;
    } else {
      end = end.prev;
    }
  }

  return pairs;
};

const findEnd = (head) => {
  let current = head;

  while (current !== null && current.next !== null) {
    current = current.next;
  }

  return current;
};

```
