

```js
const isIdenticalTree = (p, q) => {
    // Base case: Both trees are empty, so they are identical
    if (!p && !q) return true;

    // If one tree is empty and the other is not, they are not identical
    if (!p || !q) return false;

    // Check if the current nodes have the same value
    const val = p.value === q.value;

    // Recursively check left and right subtrees
    const left = isIdenticalTree(p.left, q.left);
    const right = isIdenticalTree(p.right, q.right);

    // Return true if the current nodes are identical and left and right subtrees are identical
    return val && left && right;
};


```
