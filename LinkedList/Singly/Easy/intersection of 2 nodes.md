# Problem Statement
Given the heads of two singly linked-lists `headA` and `headB`, return the node at which the two lists intersect. If the two linked lists have no intersection at all, return `null`.

## Example 1
**Input**:
- List 1: [1,3,1,2,4]
- List 2: [3,2,4]
**Output**: 2
**Explanation**: Here, both lists intersecting nodes start from node 2.

## Example 2
**Input**:
- List 1: [1,2,7]
- List 2: [2,8,1]
**Output**: Null
**Explanation**: Here, both lists do not intersect, and thus no intersection node is present.

# Brute Force Approach
- **Time Complexity**: O(m*n)
  - **Reason**: For each node in list 2, the entire list 1 is iterated.
- **Space Complexity**: O(1)

```javascript
function intersectPoint(head1, head2) {
    if (!head1 || !head2) {
        return -1;
    }

    while (head2 !== null) {
        let temp = head1;
        while (temp !== null) {
            if (temp === head2) {
                return head2;
            }
            temp = temp.next;
        }
        head2 = head2.next;
    }

    return -1;
}
```


# Hashing Approach
## Time Complexity: O(n+m)
- Reason: Iterating through list 1 first takes O(n), then iterating through list 2 takes O(m).
## Space Complexity: O(n)
- Reason: Storing list 1 node addresses in a map.

```javascript
function findIntersectionPoint(head1, head2) {
    let hashMap = new Map();

    // Step 1: Store nodes from head1 in the map
    while (head1 !== null) {
        hashMap.set(head1, true);
        head1 = head1.next;
    }

    // Step 2: Check for intersection in head2
    while (head2 !== null) {
        if (hashMap.has(head2)) {
            return head2; // Intersection point found
        }
        head2 = head2.next;
    }

    return null; // No intersection point found
}
```

# using Optimal solution2
```js
class ListNode {
  constructor(value) {
    this.num = value;
    this.next = null;
  }
}

// Utility function to find the intersection point of two linked lists
function intersectionPresent(head1, head2) {
  let d1 = head1;
  let d2 = head2;

  while (d1 !== d2) {
    d1 = d1 === null ? head2 : d1.next;
    d2 = d2 === null ? head1 : d2.next;
  }

  return d1;
}
```