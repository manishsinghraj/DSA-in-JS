## implementation of BST

```js
class TreeNode {
    constructor(value) {
        this.value = value;
        this.left = null;
        this.right = null;
    }
}

class BinarySearchTree {
    constructor() {
        this.root = null;
    }

    // insert(value)
    insert(value) {
        const newNode = new TreeNode(value);

        if (!this.root) {
            this.root = newNode;
        } else {
            this.insertNode(this.root, newNode);
        }
    }

    insertNode(root, newNode) {
        if (newNode.value < root.value) {
            if (root.left === null) {
                root.left = newNode;
            } else {
                this.insertNode(root.left, newNode);
            }
        } else {
            if (root.right === null) {
                root.right = newNode;
            } else {
                this.insertNode(root.right, newNode);
            }
        }
    }

    // Search
    search(value) {
        return this.searchNode(this.root, value);
    }

    searchNode(root, value) {
        if (!root) {
            return false;
        }

        if (value === root.value) {
            return true;
        }

        if (value < root.value) {
            return this.searchNode(root.left, value);
        }

        return this.searchNode(root.right, value);
    }

    // Traversals
    preOrder(root = this.root) {
        if (root) {
            console.log(root.value);
            this.preOrder(root.left);
            this.preOrder(root.right);
        }
    }

    inOrder(root = this.root) {
        if (root) {
            this.inOrder(root.left);
            console.log(root.value);
            this.inOrder(root.right);
        }
    }

    postOrder(root = this.root) {
        if (root) {
            this.postOrder(root.left);
            this.postOrder(root.right);
            console.log(root.value);
        }
    }

    //BFS
    levelOrder(root = this.root) {
        var queue = [];
        queue.push(root);
        let ans = [];
        while (queue.length) {
            let level = [];
            let levelSize = queue.length;
            for (let i = 0; i < levelSize; i++) {
                let curr = queue.shift();
                level.push(curr.value);
                if (curr.left) {
                    queue.push(curr.left);
                }
                if (curr.right) {
                    queue.push(curr.right);
                }
            }
            ans.push(level);
        }
        return ans;
    }

    //Min
    min(root = this.root) {
        if (!root.left) {
            return root.value;
        } else {
            return this.min(root.left);
        }
    }

    //max
    max(root = this.root) {
        if (!root.right) {
            return root.value;
        } else {
            return this.max(root.right);
        }
    }

    //remove Node
    //3 scenarios
    //Remove Node - No children
    //Remove Node - 1 children
    //Remove Node - 2 children


    delete(value) {
        this.root = this.deleteNode(this.root, value);
    }

    deleteNode(root, value) {
        if (root === null) {
            return root;
        } else {
            if (value < root.value) {
                root.left = this.deleteNode(root.left, value);
            } else if (value > root.value) {
                root.right = this.deleteNode(root.right, value);
            } else {
                //Found the value

                //Remove Node - No children
                if (!root.left && !root.right) {
                    return null;
                }

                //Remove Node - 1 children
                if (!root.right) {
                    return root.left;
                } else if (!root.left) {
                    return root.right;
                }

                // Remove Node - 2 children
                if (root.left && root.right) {
                    // Find the minimum value in the right subtree
                    root.value = this.min(root.right);
                    // Recursively delete the node with the minimum value in the right subtree
                    root.right = this.deleteNode(root.right, root.value);
                }

            }
            return root;
        }
    }
}




// create an object for the BinarySearchTree
var BST = new BinarySearchTree();

// Inserting nodes to the BinarySearchTree
BST.insert(15);
BST.insert(25);
BST.insert(10);
BST.insert(7);
BST.insert(22);
BST.insert(17);
BST.insert(13);
BST.insert(5);
BST.insert(9);
BST.insert(27);
console.log(BST.search(99));
console.log(BST);
console.log("preOrder*************")
BST.preOrder();
console.log("inOrder*************")
BST.inOrder();
console.log("postOrder*************")
BST.postOrder();
console.log("levelOrder*************")
BST.levelOrder();
console.log("min*************")
console.log(BST.min());
console.log("max*************")
console.log(BST.max());
console.log("Delete*************")
misc(BST.levelOrder());
BST.delete(5);
misc(BST.levelOrder());


//          15
//         /  \
//        10   25
//       / \   / \
//      7  13 22  27
//     / \    /
//    5   9  17

function misc(nestedArrays) {
    // Iterate through the nested arrays and join elements with commas
    const lines = nestedArrays.map(arr => arr.join(', '));

    // Join the lines with line breaks
    const result = lines.join('\n');

    // Print the result
    console.log(result);
}

```


## how deletion of 2 node works

Certainly! Let's go through an illustration step by step:

Consider the following binary search tree (BST):

```
        10
       /  \
      5    15
     / \   / \
    3   7 12  18
```

Now, let's say we want to delete the node with the value `10`, which has two children.

### Step 1: Identify the Node to Delete

The node to delete is `10`, and it has two children.

### Step 2: Find the Minimum Value in the Right Subtree

We need to find the minimum value in the right subtree of the node to be deleted. Starting from the right child (`15`), we traverse the left branches until we reach the leftmost node, which is `12`.

### Step 3: Replace Node's Value

Replace the value of the node to be deleted (`10`) with the minimum value found in the right subtree (`12`).

```
        12
       /  \
      5    15
     / \   / \
    3   7 12  18
```

### Step 4: Recursively Delete the Minimum Value Node

Now, we recursively delete the node with the minimum value in the right subtree (`12`). Since `12` has no children, it will be simply removed.

```
        12
       /  \
      5    15
     / \      \
    3   7      18
```

### Final Result

The node with the value `10` has been successfully deleted, and the binary search tree is still valid.

This process ensures that we maintain the binary search tree property while removing a node with two children. We find a replacement node from the right subtree (in this case, the minimum value) to preserve the ordering of the tree.
