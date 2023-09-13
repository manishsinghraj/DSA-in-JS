# Valid Parentheses

## Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Every close bracket has a corresponding open bracket of the same type.
 

Example 1:

Input: s = "()"
Output: true
Example 2:

Input: s = "()[]{}"
Output: true
Example 3:

Input: s = "(]"
Output: false
 

Constraints:
1 <= s.length <= 104
s consists of parentheses only '()[]{}'.

/**
 * @param {string} s
 * @return {boolean}
 */

```js
var isValid = function(s) {
    const stack = [];
    const brackets  = {
        '(' : ')',
        '{' : '}',
        '[' : ']'
    };

    //if open bracket add to stack
    //if close bracket checkthe stack by poping the top element and compare.
    //if it is not equal then return false 

    //if stack.length  is 0 then its valid.


    for(const char of s){
        if(char in brackets){
            stack.push(char);
        }else{
            if(stack.length === 0 || brackets[stack.pop()] !== char){
                return false;
            }
        }
    }

    return stack.length === 0
};
```