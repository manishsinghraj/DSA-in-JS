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

                //Remove Node - 2 children
                root.value = this.min(root.right);
                root.right = this.deleteNode(root.right, root.value);
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