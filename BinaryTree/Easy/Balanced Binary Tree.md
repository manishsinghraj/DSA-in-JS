# Check if the Binary Tree is a Balanced Binary Tree

**Problem Statement:** Check whether the given Binary Tree is a Balanced Binary Tree or not. A binary tree is balanced if, for all nodes in the tree, the difference between the left and right subtree height is not more than 1.

**Solution 1: Naive approach**
**Time Complexity:** O(N * N) (For every node, the Height Function is called, which takes O(N) time. Hence, for every node, it becomes N * N.)
**Space Complexity:** O(1) (Extra Space) + O(H) (Recursive Stack Space where “H” is the height of the tree)

```javascript
var isBalanced = function (root) {
    // Left is balanced
    // Right is balanced
    // The difference of left and right height should be less than or equal to 1

    function height(root) {
        if (root === null) {
            return 0;
        }
        return 1 + Math.max(height(root.left), height(root.right));
    }

    if (root === null) {
        return true;
    }

    var leftH = isBalanced(root.left);
    var rightH = isBalanced(root.right);

    var diff = Math.abs(height(root.left) - height(root.right)) <= 1;

    if (leftH && rightH && diff) {
        return true;
    } else {
        return false;
    }
};
```

# (Solution 2: Post Order Traversal)

**Problem Statement:** Check whether the given Binary Tree is a Balanced Binary Tree or not. A binary tree is balanced if, for all nodes in the tree, the difference between the left and right subtree height is not more than 1.

**Solution 2: Post Order Traversal**
**Time Complexity:** O(N)
**Space Complexity:** O(1) Extra Space + O(H) Recursion Stack Space (Where “H” is the height of the binary tree)

```javascript
var isBalanced = function (root) {
    return diffHeight(root) != -1;
};

function diffHeight(root) {
    if (root === null) {
        return 0;
    }

    var leftHeight = diffHeight(root.left);
    if (leftHeight === -1) {
        return -1;
    }
    var rightHeight = diffHeight(root.right);
    if (rightHeight === -1) {
        return -1;
    }

    if (Math.abs(leftHeight - rightHeight) > 1) {
        return -1;
    }

    return 1 + Math.max(leftHeight, rightHeight);
}
