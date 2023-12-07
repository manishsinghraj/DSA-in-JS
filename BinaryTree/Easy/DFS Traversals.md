// DFS - Inorder, Preorder, Postorder

# Recursion
```js
dfsInOrder(root = this.root) {
    if (root) {
        this.dfsInOrder(root.left);
        console.log(root.value);
        this.dfsInOrder(root.right);
    }
}

dfsPreOrder(root = this.root) {
    if (root) {
        console.log(root.value);
        this.dfsPreOrder(root.left);
        this.dfsPreOrder(root.right);
    }
}

dfsPostOrder(root = this.root) {
    if (root) {
        this.dfsPostOrder(root.left);
        this.dfsPostOrder(root.right);
        console.log(root.value);
    }
}
```

#Iterative

### Iterative Inorder DFS:

```javascript
iterativeInOrder() {
    const stack = [];
    let current = this.root;

    while (current || stack.length) {
        while (current) {
            stack.push(current);
            current = current.left;
        }

        current = stack.pop();
        console.log(current.value);

        current = current.right;
    }
}
```

### Iterative Preorder DFS:

```javascript
iterativePreOrder() {
    const stack = [];
    if (this.root) stack.push(this.root);

    while (stack.length) {
        const current = stack.pop();
        console.log(current.value);

        if (current.right) stack.push(current.right);
        if (current.left) stack.push(current.left);
    }
}
```

### Iterative Postorder DFS:

```javascript
iterativePostOrder() {
    const stack1 = [];
    const stack2 = [];

    if (this.root) stack1.push(this.root);

    while (stack1.length) {
        const current = stack1.pop();
        stack2.push(current);

        if (current.left) stack1.push(current.left);
        if (current.right) stack1.push(current.right);
    }

    while (stack2.length) {
        console.log(stack2.pop().value);
    }
}
```

Certainly! You can implement iterative versions of DFS (Inorder, Preorder, and Postorder) using a stack. The idea is to mimic the recursive approach using an explicit stack to keep track of nodes to be processed.

Here are the iterative implementations:

### Iterative Inorder DFS:

```javascript
iterativeInOrder() {
    const stack = [];
    let current = this.root;

    while (current || stack.length) {
        while (current) {
            stack.push(current);
            current = current.left;
        }

        current = stack.pop();
        console.log(current.value);

        current = current.right;
    }
}
```

### Iterative Preorder DFS:

```javascript
iterativePreOrder() {
    const stack = [];
    if (this.root) stack.push(this.root);

    while (stack.length) {
        const current = stack.pop();
        console.log(current.value);

        if (current.right) stack.push(current.right);
        if (current.left) stack.push(current.left);
    }
}
```

### Iterative Postorder DFS:

```javascript
iterativePostOrder() {
    const stack1 = [];
    const stack2 = [];

    if (this.root) stack1.push(this.root);

    while (stack1.length) {
        const current = stack1.pop();
        stack2.push(current);

        if (current.left) stack1.push(current.left);
        if (current.right) stack1.push(current.right);
    }

    while (stack2.length) {
        console.log(stack2.pop().value);
    }
}
```

These iterative approaches use a stack to simulate the function call stack in the recursive versions. 
The key is to properly manage the order in which nodes are processed and pushed onto the stack.
The iterative approach helps avoid the function call overhead and can be useful in scenarios where you want to avoid recursion 
or if your environment has limitations on the maximum call stack size.
