## Detect a Cycle in a Linked List

**Problem Statement:**

Given head, the head of a linked list, determine if the linked list has a cycle in it. There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer.

Return true if there is a cycle in the linked list. Otherwise, return false.

**Example 1:**

**Input:**
Head = [1, 2, 3, 4]
**Output:**
true
**Explanation:**
Here, we can see that we can reach node at position 1 again by following the next pointer. Thus, we return true for this case.

**Example 2:**

**Input:**
Head = [1, 2, 3, 4]
**Output:**
false
**Explanation:**
Neither of the nodes present in the given list can be visited again by following the next pointer. Hence, no loop exists. Thus, we return false.

**Solution: Hashing**

**Time Complexity:** O(N)
- **Reason:** Entire list is iterated once.

**Space Complexity:** O(N)
- **Reason:** All nodes present in the list are stored in a hash table.

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */

/**
 * @param {ListNode} head
 * @return {boolean}
 */

var hasCycle = function(head) {
    let current = head;
    var hashMap = new Map();
    var cycleExist = false;

    while (current) {
        if (hashMap.get(current)) {
            cycleExist = true;
            break;
        } else {
            hashMap.set(current, true);
        }
        current = current.next;
    }
    return cycleExist;
};
```

## Detect a Cycle in a Linked List (Using Floyd's Cycle Detection Algorithm)

**Time Complexity:** O(N)
- **Reason:** In the worst case, all the nodes of the list are visited.

**Space Complexity:** O(1)
- **Reason:** No extra data structure is used.

```javascript
var hasCycle = function(head) {
    if(head == null){
        return false;
    }

    fast = head.next;
    slow = head;

    while(fast != null && slow != null){
        if(fast == slow){
            return true;
        }

        if(fast.next == null) return false;

        fast = fast.next.next;
        slow = slow.next;
    }
    return false;
};
```

## Detect the Entry Point of a Cycle in a Linked List

```javascript
function detectCycle(head) {
    if (!head || !head.next) {
        return null; // No cycle if the list is empty or has only one node
    }

    // Step 1: Detect the cycle and find the point of intersection
    let tortoise = head;
    let hare = head;
    let intersection = null;

    while (hare && hare.next) {
        tortoise = tortoise.next; // Move one step
        hare = hare.next.next;  // Move two steps

        if (tortoise === hare) {
            intersection = tortoise; // Point of intersection
            break;
        }
    }

    if (!intersection) {
        return null; // No cycle found
    }

    // Step 2: Find the entry point of the cycle
    tortoise = head; // Reset tortoise to the head

    while (tortoise !== hare) {
        tortoise = tortoise.next;
        hare = hare.next;
    }

    return tortoise; // Entry point of the cycle
}
```

#Detect and remove the cycle connection
```js
function detectAndRemoveLoop(head) {
    let slow = head;
    let fast = head;

    // Detect whether a loop exists
    while (slow !== null && fast !== null && fast.next !== null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow === fast) {
            break; // Loop detected
        }
    }

    if (slow === fast) {
        // If a loop is detected, find the start of the loop
        slow = head;
        while (slow !== fast) {
            slow = slow.next;
            fast = fast.next;
        }

        // Remove the loop by breaking the link
        while (fast.next !== slow) {
            fast = fast.next;
        }
        fast.next = null;
    }
}
```