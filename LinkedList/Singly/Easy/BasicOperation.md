## Search an element in a Linked List (Iterative and Recursive)

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



## Find Length of a Linked List (Iterative and Recursive)


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


## Linked List Deletion (Deleting a given key)


`refer Implementation of LL`

## Linked List Deletion (Deleting a key at given position)


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

  deleteAtPosition(position) {
    if (position < 0) {
      console.log("Invalid position");
      return;
    }

    if (position === 0) {
      this.head = this.head.next;
      return;
    }

    let current = this.head;
    let count = 0;

    while (current && count < position - 1) {
      current = current.next;
      count++;
    }

    if (!current || !current.next) {
      console.log("Position out of range");
      return;
    }

    current.next = current.next.next;
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

myList.deleteAtPosition(2); // Deleting node at position 2

console.log("Linked List after deletion:");
myList.print();

```

## Write a function to get Nth node in a Linked List



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

  getNthNode(n) {
    if (n < 1) {
      console.log("Invalid value of N");
      return null;
    }

    let current = this.head;
    let count = 1;

    while (current && count < n) {
      current = current.next;
      count++;
    }

    if (!current) {
      console.log("N is greater than the length of the list");
      return null;
    }

    return current;
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

const nthNode = myList.getNthNode(2); // Getting the 2nd node
if (nthNode) {
  console.log("Nth Node:", nthNode.val);
}

```

## Nth node from the end of a Linked List


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

## Print the middle of a given linked list


```js 
const middleOfLL = (head) => {
	let current = head;
	let count = 0;
	
	while(current){
		count++;
		current = current.next;
}

let result = this.head;

for(let i = 0; i < Math.floor(count/2); i++){
	result = result.next;
}

return result;
}
```
`"console.log(5/2) = 2.5.   
console.log(Math.floor(5/2)) = 2"`

Refer this
```js 
const middleOfLL = (head) => {
    let slow = head;
    let fast = head;

    // Move 'fast' two steps and 'slow' one step until 'fast' reaches the end
    while (fast && fast.next) {
        slow = slow.next;
        fast = fast.next.next;
    }

    // 'slow' is now at the middle of the linked list
    return slow;
};

```

## Counts the number of times a given int occurs in a Linked List


```js 
//just traverse and check if val matched keep tract of count and return.
```


## Check if a linked list is Circular Linked List


```js 
const checkCircularLL = (head) => {
    if (!head) return false;

    let fast = head;
    let slow = head;

    while (fast && fast.next) {
        fast = fast.next.next;
        slow = slow.next;

        if (fast === slow) {
            return true; // The linked list is circular
        }
    }

    return false; // The linked list is not circular
};

```

## Count nodes in Circular linked list


```js 
const countNodesInCircularLL = (head) => {
    if (!head) return 0;

    let count = 1;
    let current = head.next;

    while (current && current !== head) { //Trick is here
        count++;
        current = current.next;
    }

    return count;
};

```


## Convert singly linked list into circular linked list



```js 
const singlyToCircularLL = (head) => {
  if (!head) return null;

  let current = head;

  while (current.next) {
    current = current.next;
  }

  current.next = head;

  return head;
}

```

## Exchange first and last nodes in Circular Linked List


#### difficult to visualize

```js 
class Node {
  constructor(val) {
    this.val = val;
    this.next = null;
  }
}

const exchangeFirstAndLast = (head) => {
  if (!head || !head.next || !head.next.next) {
    return head;
  }

  let current = head;

  while (current.next.next !== head) {
    current = current.next;
  }

  // Save the last node
  let last = current.next;

  // Make the last node the new head
  current.next = head;
  head = last;

  // Update the next of the original first node
  last.next = head.next;
  head.next = last;

  return head;
};

```

