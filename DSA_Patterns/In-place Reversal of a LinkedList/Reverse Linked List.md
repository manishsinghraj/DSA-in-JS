# Reverse Linked List

## Given the head of a singly linked list, reverse the list, and return the reversed list.

<br>

Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]

<br>

Input: head = [1,2]
Output: [2,1]

<br>
Example 3:

Input: head = []
Output: []
<br>

Constraints:

The number of nodes in the list is the range [0, 5000].
-5000 <= Node.val <= 5000
 <br>

Follow up: A linked list can be reversed either iteratively or recursively. Could you implement both?

<br>

```js
var reverseList = function(head) {
      if(!head){
          return null;
      }

      let previous = null;
      let current = head;

      while(current){
          let nextNode = current.next;
          current.next = previous;
          previous = current;
          current = nextNode
      }

      return previous;
};
```
