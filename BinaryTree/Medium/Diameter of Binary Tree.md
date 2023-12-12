# Diameter of Binary Tree

- Longest Path between the 2 nodes
- it is not necessary that it needs to pass through root

  

Given the root of a binary tree, return the length of the diameter of the tree.

The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

The length of a path between two nodes is represented by the number of edges between them.

 

Example 1:


Input: root = [1,2,3,4,5]
Output: 3
Explanation: 3 is the length of the path [4,2,1,3] or [5,2,1,3].
Example 2:

Input: root = [1,2]
Output: 1
 

Constraints:

The number of nodes in the tree is in the range [1, 104].
-100 <= Node.val <= 100



o(n^2)
```js
const diameterOfTree = (root) => {
    if (!root) return 0;

    let diameter = 0;

    const leftHeight = height(root.left);
    const rightHeight = height(root.right);

    diameter = Math.max(diameter, leftHeight + rightHeight);

    return diameter;
}

const height = (root) => {
    if (!root) return 0;

    const left = height(root.left);
    const right = height(root.right);

    return 1 + Math.max(left, right);
}


```

o(n)
```js
var diameterOfBinaryTree = function(root) {
	if(!root) return 0;

	let result = {diameter : 0};

	height(root, result);

	return result.diameter;

}

var height= function(root, result){
	if(!root) return 0;

	const leftHeight = height(root.left, result);
	const rightHeight = height(root.right, result);

	result.diameter = Math.max(result.diameter, leftHeight + rightHeight);

	return 1 + Math.max(leftHeight,rightHeight);

}


```

The line `let result = {diameter: 0};` initializes an object `result` with a property `diameter` set to 0. This approach is commonly used in JavaScript to create an object with a default value.

In this particular case, the `result` object is used to store the maximum diameter encountered during the recursion. The reason for using an object with a property is that primitive values (like numbers) are passed by value in JavaScript, meaning that changes to the parameter within the recursive calls wouldn't persist outside of the current function call.

By using an object, you are passing a reference to the object itself. This way, changes made to the object's properties inside the recursive calls are visible outside of the function, and you can effectively use it to store and update the maximum diameter.

Here's how it works in the given code:

```javascript
let result = {diameter: 0};
```

This line creates an object `result` with an initial `diameter` value of 0.

```javascript
height(root, result);
```

The `result` object is then passed to the `height` function, where it's used to store and update the maximum diameter.

```javascript
return result.diameter;
```

Finally, the function returns the maximum diameter stored in the `result` object.

In summary, using an object to store the result allows you to maintain state across recursive calls and update values effectively. It's a common technique in JavaScript when you need to modify values within a function and have those changes reflected outside the function.
