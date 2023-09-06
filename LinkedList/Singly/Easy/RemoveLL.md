# Remove Nodes with Specific Value from Linked List

Given the head of a linked list and an integer val, remove all the nodes of the linked list that have Node.val equal to val, and return the new head.

## Example 1:

Input: `head = [1,2,6,3,4,5,6], val = 6`
Output: `[1,2,3,4,5]`

## Example 2:

Input: `head = [], val = 1`
Output: `[]`

## Example 3:

Input: `head = [7,7,7,7], val = 7`
Output: `[]`

## Constraints:

- The number of nodes in the list is in the range [0, 104].
- 1 <= Node.val <= 50
- 0 <= val <= 50


Time Complexity (TC):
The time complexity of this algorithm is O(n), where n is the number of nodes in the linked list. It iterates through the linked list once to remove nodes with the given value.

Space Complexity (SC):
The space complexity is O(1) because the algorithm uses a constant amount of extra space regardless of the size of the linked list. It uses only a few additional pointers (current, previous, and val) to perform the removals, and the space used does not depend on the input size.

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val === undefined ? 0 : val)
 *     this.next = (next === undefined ? null : next)
 * }
 */

/**
 * Remove all nodes with a given value from a linked list.
 * @param {ListNode} head - The head of the linked list.
 * @param {number} val - The value to be removed.
 * @return {ListNode} - The new head of the modified linked list.
 */
var removeElements = function(head, val) {
    if (!head) {
        return null;
    }
    
    let current = head;
    let previous = null;
    
    while (current) {
        if (current.val === val) {
            if (previous) {
                previous.next = current.next;
            } else {
                head = current.next;
            }
        } else {
            previous = current;
        }
        current = current.next;
    }
    
    return head;
};
```


## Using Recursion

This recursive solution also has a time complexity of O(n), but it may have better space complexity in some cases as it doesn't use an explicit loop with extra pointers. Instead, it leverages the call stack for recursion.

Both the iterative and recursive solutions are efficient and optimized for this problem, and you can choose the one that fits your coding style and preferences.

```js
var removeElements = function(head, val) {
    if (!head) {
        return null;
    }

    head.next = removeElements(head.next, val);
    return head.val === val ? head.next : head;
};
```

