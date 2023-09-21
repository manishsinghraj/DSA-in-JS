# Maximum Depth of a Binary Tree

**Problem Statement:** Find the Maximum Depth of Binary Tree. Maximum Depth is the count of nodes of the longest path from the root node to the leaf node.

## Using Recursion

```javascript
// Time Complexity: O(N)
// Space Complexity: O(1) Extra Space + O(H) Recursion Stack space, where “H” is the height of the binary tree.

var maxDepth = function (root) {
    if (root === null) {
        return 0;
    }

    const leftHeight = maxDepth(root.left);
    const rightHeight = maxDepth(root.right);

    return 1 + Math.max(leftHeight, rightHeight);
};

```

# Using Queue

**Time Complexity:** O(N)
**Space Complexity:** O(N) (Queue data structure is used)

```javascript
class TreeNode {
    constructor(val) {
        this.val = val;
        this.left = null;
        this.right = null;
    }
}

function maxDepth(root) {
    if (!root) {
        return 0;
    }

    const queue = [];
    queue.push(root);

    let level = 0;

    while (queue.length > 0) {
        const size = queue.length;

        for (let i = 0; i < size; i++) {
            const remNode = queue.shift();
            if (remNode.left !== null) {
                queue.push(remNode.left);
            }
            if (remNode.right !== null) {
                queue.push(remNode.right);
            }
        }

        level++;
    }

    return level;
}

// Example usage:
const root = new TreeNode(3);
root.left = new TreeNode(9);
root.right = new TreeNode(20);
root.right.left = new TreeNode(15);
root.right.right = new TreeNode(7);

const depth = maxDepth(root);
console.log(depth); // Output: 3
