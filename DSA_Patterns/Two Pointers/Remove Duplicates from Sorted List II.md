# Remove Duplicates from Sorted List II


Given the head of a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list. Return the linked list sorted as well.
<br>
Input: head = [1,2,3,3,4,4,5]
Output: [1,2,5]
<br>


Input: head = [1,1,1,2,3]
Output: [2,3]
 <br>

Constraints:

The number of nodes in the list is in the range [0, 300].
-100 <= Node.val <= 100
The list is guaranteed to be sorted in ascending order.
<br>

```js
var deleteDuplicates = function(head) {
    if(!head) return null;

    let dummyNode = new ListNode(0);

    dummyNode.next = head;

    let list = dummyNode;

    while(list.next!== null && list.next.next!==null){
        if(list.next.val === list.next.next.val){
            while(list.next && list.next.next && list.next.val === list.next.next.val){
                list.next = list.next.next;
            }
            list.next = list.next.next;
        } else {
            list = list.next;
        }
    }

    return dummyNode.next;
};
```
