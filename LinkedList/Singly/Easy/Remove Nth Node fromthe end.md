## Remove N-th Node from the End of a Linked List
// Traversing Twice
// Time Complexity (TC): O(N)
// Space Complexity (SC): O(1)
```javascript
function removeNthFromEnd(head, n) {
    let current = head;
    let length = 0;

    while (current) {
        current = current.next;
        length++;
    }

    let positionToBeRemoved = length - n;

    if (positionToBeRemoved === 0) {
        return head.next;
    }

    let prev = null;
    let currentPosition = 0;
    current = head;

    while (currentPosition !== positionToBeRemoved) {
        prev = current;
        currentPosition++;
        current = current.next;
    }

    prev.next = current.next;
    return head;
}
```


## Remove N-th Node from the End of a Linked List (Optimal Solution)

```javascript
// Optimal Solution
// Time Complexity (TC): O(N)
// Space Complexity (SC): O(1)

function removeNthFromEnd(head, n) {
    let dummy = new ListNode(0);
    dummy.next = head;
    let first = dummy;
    let second = dummy;

    // Move the first pointer n+1 steps ahead
    for (let i = 0; i <= n; i++) {
        first = first.next;
    }

    // Move first to the end, maintaining the gap
    while (first !== null) {
        first = first.next;
        second = second.next;
    }

    // Remove the N-th node from the end
    second.next = second.next.next;

    return dummy.next;
}
```
