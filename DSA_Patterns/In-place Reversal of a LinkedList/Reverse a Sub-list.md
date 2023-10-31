# Reverse Linked List II

## Given the head of a singly linked list and two integers left and right where left <= right, reverse the nodes of the list from position left to position right, and return the reversed list.


 <br>

 Input: head = [1,2,3,4,5], left = 2, right = 4
Output: [1,4,3,2,5]

 <br>
Example 2:

Input: head = [5], left = 1, right = 1
Output: [5]
  <br>

Constraints:

The number of nodes in the list is n.
1 <= n <= 500
-500 <= Node.val <= 500
1 <= left <= right <= n
  <br>

  

Follow up: Could you do it in one pass?


```js
//Two Pointers
var reverseBetween = function(head, left, right) {
    if (!head || left === right) return head;

    let dummy = new ListNode(0);
    dummy.next = head;
    let prevL = dummy;

    for (let i = 0; i < left - 1; i++) {
        prevL = prevL.next;
    }

    let current = prevL.next;
    let previous = null;
    let nextNode = null;

    for (let i = 0; i < right - left + 1; i++) {
        nextNode = current.next;
        current.next = previous;
        previous = current;
        current = nextNode;
    }

    // Connect the last node in the reversed section to the node after 'right'.
    prevL.next.next = current;

    // Connect 'left - 1' to the first node in the reversed section.
    prevL.next = previous;

    return dummy.next;
};


```

```js
//Using Stack
var reverseBetween = function(head, left, right) {
    if (!head || left === right) return head;

    let dummy = new ListNode(0);
    dummy.next = head;
    let prevL = dummy;
    let stack = [];

    // Move to the (left-1) position
    for (let i = 0; i < left - 1; i++) {
        prevL = prevL.next;
    }

    // Push nodes between left and right onto the stack
    let current = prevL.next;
    for (let i = left; i <= right; i++) {
        stack.push(current);
        current = current.next;
    }

    // Pop nodes from the stack and reconnect them
    while (stack.length > 0) {
        prevL.next = stack.pop();
        prevL = prevL.next;
    }

    // Connect the last node in the reversed section to the node after 'right'.
    prevL.next = current;

    return dummy.next;
};
```
