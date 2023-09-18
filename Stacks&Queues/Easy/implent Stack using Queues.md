## Implement Stack using Queues (Two Queues)
// Steps:
// Push ::
// 1. Add x -> q2
// 2. q1 - > q2 (element by element)
// 3. swap q1 and q2
### Push Operation:

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

In the push method, when you enqueue an element, you need to rearrange all the elements in queue1 so that the newly added element becomes the front of the queue. This requires iterating over queue1 and moving elements to queue2. The time complexity of this operation is O(n), where n is the number of elements in the queue. The space complexity is O(1) because you are not using additional memory proportional to the size of the input; you're only rearranging the existing elements.

### Pop Operation:

- **Time Complexity:** O(1)
- **Space Complexity:** O(1)

The pop operation simply dequeues an element from the front of queue1. Since there is no rearranging of elements involved, the time complexity is O(1). The space complexity is also O(1) because no additional memory is used.

### Top Operation:

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

The top operation is similar to the push operation as it also involves rearranging elements in queue1. You need to move elements from queue1 to queue2 until you reach the last element. This takes O(n) time, where n is the number of elements in the queue. The space complexity is O(1) because you're not using additional memory proportional to the size of the input.

### isEmpty Operation:

- **Time Complexity:** O(1)
- **Space Complexity:** O(1)

Checking if the stack is empty by examining the length of queue1 is a constant-time operation, so it's O(1). The space complexity is also O(1) because no additional memory is used.

### Size Operation:

- **Time Complexity:** O(1)
- **Space Complexity:** O(1)

Getting the size of the stack by examining the length of queue1 is a constant-time operation, so it's O(1). The space complexity is also O(1) because no additional memory is used.

### Code:

```javascript
class StackUsingQueue {
    constructor() {
        this.queue1 = [];
        this.queue2 = [];
    }

    // Push an element onto the stack
    push(element) {
        // Enqueue the new element into queue1
        this.queue1.push(element);
    }

    // Pop an element from the stack
    pop() {
        if (this.isEmpty()) {
            return "Stack is empty";
        }

        // Move elements from queue1 to queue2, leaving one element in queue1
        while (this.queue1.length > 1) {
            this.queue2.push(this.queue1.shift());
        }

        // Pop and return the last element in queue1 (equivalent to popping from the stack)
        const poppedElement = this.queue1.shift();

        // Swap the names of queue1 and queue2 to maintain consistency
        [this.queue1, this.queue2] = [this.queue2, this.queue1];

        return poppedElement;
    }

    // Return the top element without removing it
    top() {
        if (this.isEmpty()) {
            return "Stack is empty";
        }

        // Move elements from queue1 to queue2 until we reach the last element
        while (this.queue1.length > 1) {
            this.queue2.push(this.queue1.shift());
        }

        // Get the last element in queue1 (the top of the stack)
        const topElement = this.queue1[0];

        // Re-enqueue it into queue2 to maintain consistency
        this.queue2.push(this.queue1.shift());

        // Swap the names of queue1 and queue2 to maintain consistency
        [this.queue1, this.queue2] = [this.queue2, this.queue1];

        return topElement;
    }

    // Check if the stack is empty
    isEmpty() {
        return this.queue1.length === 0;
    }

    // Return the size of the stack
    size() {
        return this.queue1.length;
    }
}

// Example usage:
const stack = new StackUsingQueue();

stack.push(1);
stack.push(2);
stack.push(3);

console.log("Top:", stack.top()); // Output: Top: 3
console.log("Pop:", stack.pop()); // Output: Pop: 3
console.log("Top:", stack.top()); // Output: Top: 2

```

## Implement Stack using Queue (One Queue)

### Push Operation:

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

In the push method, when you enqueue an element, you need to rearrange all the elements in the queue so that the newly added element becomes the front of the queue. This requires iterating over the entire queue and moving elements to the end of the queue. As a result, the time complexity of this operation is O(n), where n is the number of elements in the queue. The space complexity is also O(n) because you temporarily use additional memory proportional to the size of the queue while rearranging the elements.

### Pop Operation:

- **Time Complexity:** O(1)
- **Space Complexity:** O(1)

The pop operation simply dequeues an element from the front of the queue. Since there is no rearranging of elements involved, the time complexity is O(1). The space complexity is also O(1) because no additional memory is used.

### Top Operation:

- **Time Complexity:** O(1)
- **Space Complexity:** O(1)

The top operation returns the front element of the queue without removing it, which is a constant-time operation, so it's O(1). The space complexity is also O(1) because no additional memory is used.

### isEmpty Operation:

- **Time Complexity:** O(1)
- **Space Complexity:** O(1)

Checking if the stack is empty by examining the length of the queue is a constant-time operation, so it's O(1). The space complexity is also O(1) because no additional memory is used.

### Size Operation:

- **Time Complexity:** O(1)
- **Space Complexity:** O(1)

Getting the size of the stack by examining the length of the queue is a constant-time operation, so it's O(1). The space complexity is also O(1) because no additional memory is used.

### Code:

```javascript
class StackUsingQueue {
    constructor() {
        this.queue = [];
    }

    // Push an element onto the stack
    push(element) {
        // Enqueue the new element into the queue
        this.queue.push(element);

        // Rearrange the queue to simulate a stack
        const size = this.queue.length;
        for (let i = 0; i < size - 1; i++) {
            this.queue.push(this.queue.shift());
        }
    }

    // Pop an element from the stack
    pop() {
        if (this.isEmpty()) {
            return "Stack is empty";
        }
        return this.queue.shift();
    }

    // Return the top element without removing it
    top() {
        if (this.isEmpty()) {
            return "Stack is empty";
        }
        return this.queue[0];
    }

    // Check if the stack is empty
    isEmpty() {
        return this.queue.length === 0;
    }

    // Return the size of the stack
    size() {
        return this.queue.length;
    }
}

// Example usage:
const stack = new StackUsingQueue();

stack.push(1);
stack.push(2);
stack.push(3);

console.log("Top:", stack.top()); // Output: Top: 3
console.log("Pop:", stack.pop()); // Output: Pop: 3
console.log("Top:", stack.top()); // Output: Top: 2
```