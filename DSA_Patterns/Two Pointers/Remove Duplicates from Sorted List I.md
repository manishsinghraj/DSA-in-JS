# Remove Duplicates from Sorted List 1


## Given the head of a sorted linked list, delete all duplicates such that each element appears only once. Return the linked list sorted as well.

Input: head = [1,1,2]
Output: [1,2]

Input: head = [1,1,2,3,3]
Output: [1,2,3]
 

Constraints:

The number of nodes in the list is in the range [0, 300].
-100 <= Node.val <= 100
The list is guaranteed to be sorted in ascending order.


```js
var deleteDuplicates = function(head) {

    if(head == null || head.next == null)
        return head;

    let current = head;

    while(current != null && current.next != null){
        if(current.val === current.next.val){
            current.next = current.next.next; 
        } else {
            current = current.next;
        }
    }

    return head;
    
};
```
