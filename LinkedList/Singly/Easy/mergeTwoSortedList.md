# Merge Two Sorted Linked Lists

## Problem Statement

Given two singly linked lists that are sorted in increasing order of node values, merge them into a single sorted list by splicing together the nodes of the first two lists.

**Example:**

**Input:**
List 1: {3, 7, 10}
List 2: {1, 2, 5, 8, 10}

**Output:**
Merged List: {1, 2, 3, 5, 7, 8, 10, 10}

## Time Complexity (TC) and Space Complexity (SC)

- **Time Complexity (TC):** O(n + m), where n is the length of the first list (l1), and m is the length of the second list (l2). This is because we traverse both input linked lists once, comparing and merging nodes in a single pass.

- **Space Complexity (SC):** O(n + m), where n is the length of the first list (l1), and m is the length of the second list (l2). This is because we create a new linked list to store the merged result, and the space required for this new linked list depends on the lengths of both input lists. Additionally, we use a constant amount of additional space for pointers and temporary variables, which does not depend on the input sizes.

## JavaScript Implementation

```javascript
class ListNode {
    constructor(val, next = null) {
        this.val = val;
        this.next = next;
    }
}

function mergeSortedLists(l1, l2) {
    var dummy = new Node();
    let current = dummy;

    while (l1 !== null && l2 !== null) {
        if (l1.val < l2.val) {
            current.next = l1;
            l1 = l1.next;
        } else {
            current.next = l2;
            l2 = l2.next;
        }
        current = current.next;
    }

    if (l1) {
        current.next = l1;
    } else {
        current.next = l2;
    }
    return dummy.next;
}

// Helper functions to create and convert linked lists

function createLinkedListFromArray(arr) {
    let dummy = new ListNode();
    let current = dummy;
    for (const val of arr) {
        current.next = new ListNode(val);
        current = current.next;
    }
    return dummy.next;
}

function convertLinkedListToArray(head) {
    const result = [];
    let current = head;
    while (current) {
        result.push(current.val);
        current = current.next;
    }
    return result;
}

// Test cases

function testMergeSortedLists(list1, list2) {
    const mergedList = mergeSortedLists(list1, list2);
    const mergedArray = convertLinkedListToArray(mergedList);
    console.log("List 1:", convertLinkedListToArray(list1));
    console.log("List 2:", convertLinkedListToArray(list2));
    console.log("Merged List:", mergedArray);
    console.log("------------------------");
}

const list1 = createLinkedListFromArray([1, 3, 5]);
const list2 = createLinkedListFromArray([2, 4, 6]);
testMergeSortedLists(list1, list2);

const list3 = createLinkedListFromArray([1, 2, 4]);
const list4 = createLinkedListFromArray([1, 3, 4]);
testMergeSortedLists(list3, list4);

const list5 = createLinkedListFromArray([10, 20, 30]);
const list6 = createLinkedListFromArray([5, 15, 25]);
testMergeSortedLists(list5, list6);
```


## Optimal Solution

**Time Complexity:**

We are still traversing both lists entirely in the worst-case scenario. So, it remains the same as O(N+M), where N is the number of nodes in list 1 and M is the number of nodes in list 2.

**Space Complexity:**

We are using the same lists just changing links to create our desired list. So no extra space is used. Hence, its space complexity is O(1).

```javascript
class ListNode {
    constructor(val) {
        this.val = val;
        this.next = null;
    }
}

class Solution {
    mergeTwoLists(l1, l2) {
        // When list1 is empty, the output will be the same as list2
        if (!l1) {
            return l2;
        }

        // When list2 is empty, the output will be the same as list1
        if (!l2) {
            return l1;
        }

        // Pointing l1 and l2 to the smallest and greatest nodes
        if (l1.val > l2.val) {
            [l1, l2] = [l2, l1];
        }

        // Act as the head of the resultant merged list
        let res = l1;

        while (l1 !== null && l2 !== null) {
            let temp = null;
            while (l1 !== null && l1.val <= l2.val) {
                temp = l1; // storing the last sorted node
                l1 = l1.next;
            }
            // Link the previous sorted node with the next larger node in list2
            temp.next = l2;
            [l1, l2] = [l2, l1];
        }
        return res;
    }
}
```