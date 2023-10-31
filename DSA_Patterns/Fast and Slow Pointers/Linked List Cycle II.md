# Linked List Cycle II.md

## Given the head of a linked list, return the node where the cycle begins. If there is no cycle, return null.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to (0-indexed). It is -1 if there is no cycle. Note that pos is not passed as a parameter.

Do not modify the linked list.

<br>

Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.
Example 2:

<br>

Input: head = [1,2], pos = 0
Output: tail connects to node index 0
Explanation: There is a cycle in the linked list, where tail connects to the first node.

<br>

Input: head = [1], pos = -1
Output: no cycle
Explanation: There is no cycle in the linked list.
<br>

Constraints:

The number of the nodes in the list is in the range [0, 104].
-105 <= Node.val <= 105
pos is -1 or a valid index in the linked-list.
 <br>

Follow up: Can you solve it using O(1) (i.e. constant) memory?

<br>

```js
var detectCycle = function(head) {
    if(!head) return null;

    let slow = head;
    let fast = head;
    let hasCycle = false;

    while(fast!==null && fast.next!==null){
        slow = slow.next;
        fast = fast.next.next;

        if(slow === fast){
            hasCycle = true;
            break;
        }
    }

    if(!hasCycle) return null;

    slow = head;

    while(slow!==fast){
        slow = slow.next;
        fast = fast.next;
    }

    return slow;
};

```
