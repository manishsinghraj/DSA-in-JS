```js
class Node {
  constructor(val) {
    this.val = val;
    this.next = null;
  }
}

const intersectionOfSortedList = (head1, head2) => {
  if (!head1 || !head2) return null;

  let current = head1;
  const myMap = new Map();

  // Store values from the first list in a map
  while (current !== null) {
    myMap.set(current.val, true);
    current = current.next;
  }

  current = head2;
  let result = [];

  // Check for intersection while traversing the second list
  while (current !== null) {
    let currentValue = current.val;
    if (myMap.has(currentValue)) {
      result.push(current.val);
    }
    current = current.next;
  }

  return result.join(" -> ");
};

// Example usage:
// Create two sorted linked lists: 1 -> 2 -> 4 and 2 -> 4 -> 6
let list1 = new Node(1);
list1.next = new Node(2);
list1.next.next = new Node(4);

let list2 = new Node(2);
list2.next = new Node(4);
list2.next.next = new Node(6);

// Call the function to find the intersection
let intersection = intersectionOfSortedList(list1, list2);

console.log(intersection);

```

# Optimal
```js
class Node {
  constructor(val) {
    this.val = val;
    this.next = null;
  }
}

const intersectionOfSortedList = (head1, head2) => {
  if (!head1 || !head2) return null;

  let result = [];
  let pointer1 = head1;
  let pointer2 = head2;

  while (pointer1 !== null && pointer2 !== null) {
    if (pointer1.val === pointer2.val) {
      result.push(pointer1.val);
      pointer1 = pointer1.next;
      pointer2 = pointer2.next;
    } else if (pointer1.val < pointer2.val) {
      pointer1 = pointer1.next;
    } else {
      pointer2 = pointer2.next;
    }
  }

  return result.join(" -> ");
};

// Example usage:
// Create two sorted linked lists: 1 -> 2 -> 4 and 2 -> 4 -> 6
let list1 = new Node(1);
list1.next = new Node(2);
list1.next.next = new Node(4);

let list2 = new Node(2);
list2.next = new Node(4);
list2.next.next = new Node(6);

// Call the function to find the intersection
let intersection = intersectionOfSortedList(list1, list2);

console.log(intersection);

```
