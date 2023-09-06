# Function to find the second middle of the linked list.


### Brute Force Approach

# Time Complexity (TC)
The time complexity of this brute-force approach is O(n), where n is the number of nodes in the linked list. This is because it iterates through the entire linked list once to count the nodes and then moves the current pointer to the middle node.

# Space Complexity (SC)
The space complexity is O(1) because it uses a constant amount of extra space to store variables (`count` and `current`) regardless of the size of the linked list.


```js
class ListNode {
    constructor(val) {
        this.val = val;
        this.next = null;
    }
}

/**
 * Find the second middle element of a linked list.
 * @param {ListNode} head - The head of the linked list.
 * @returns {ListNode} - The second middle node.
 */
function secondMiddleOfLinkedList(head) {
    let count = 0;
    let current = head;

    // Count the number of nodes in the linked list.
    while (current !== null) {
        count++;
        current = current.next;
    }

    current = head;

    // Move the current pointer to the middle node.
    for (let i = 0; i < Math.floor(count / 2); i++) {
        current = current.next;
    }

    return current;
}

// Example usage:
// Create the linked list: 1 -> 2 -> 3 -> 4 -> 5 -> 6
const head2 = new ListNode(1);
head2.next = new ListNode(2);
head2.next.next = new ListNode(3);
head2.next.next.next = new ListNode(4);
head2.next.next.next.next = new ListNode(5);
head2.next.next.next.next.next = new ListNode(6);

const secondMiddle2 = secondMiddleOfLinkedList(head2);
console.log("Second middle of the second linked list:", secondMiddle2.val); // Output: 4
```

# Optimizations
This brute-force approach can be optimized to find the second middle element of a linked list in a single pass using two pointers (fast and slow pointers) without counting the number of nodes. This approach would have the same time complexity but would be more efficient in terms of runtime.

In this optimized code, we use two pointers, slow and fast, to traverse the linked list. The slow pointer advances one step at a time, while the fast pointer advances two steps at a time. When the fast pointer reaches the end of the list, the slow pointer will be at the middle of the list, and this approach eliminates the need to count the nodes or make multiple passes through the list.

The time complexity of this optimized approach is still O(n), but it is more efficient than the brute-force approach, especially for large linked lists.

# Optimized Code to Find the Second Middle of a Linked List

To find the second middle element of a linked list more efficiently without counting the number of nodes, you can use two pointers: a slow pointer and a fast pointer.

```javascript
// Function to find the second middle of the linked list using two pointers.

/**
 * Find the second middle element of a linked list.
 * @param {ListNode} head - The head of the linked list.
 * @returns {ListNode} - The second middle node.
 */
function secondMiddleOfLinkedList(head) {
    let slow = head;
    let fast = head;

    while (fast !== null && fast.next !== null) {
        slow = slow.next;
        fast = fast.next.next;
    }

    return slow;
}

// Example usage:
// Create the linked list: 1 -> 2 -> 3 -> 4 -> 5 -> 6
const head = new ListNode(1);
head.next = new ListNode(2);
head.next.next = new ListNode(3);
head.next.next.next = new ListNode(4);
head.next.next.next.next = new ListNode(5);
head.next.next.next.next.next = new ListNode(6);

const secondMiddle = secondMiddleOfLinkedList(head);
console.log("Second middle of the linked list:", secondMiddle.val); // Output: 3
