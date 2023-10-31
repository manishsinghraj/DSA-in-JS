# Given a string s, find the length of the longest substring without repeating characters.


Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.


Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.

Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
 
<br>
Constraints:

0 <= s.length <= 5 * 104
s consists of English letters, digits, symbols and spaces.

```js
//o(n^2) //o(m)
var lengthOfLongestSubstringBruteForce = function(s) {
    if (s.length === 0) return 0;

    let maxLength = 0;

    for (let i = 0; i < s.length; i++) {
        let charSet = new Set();
        let currentLength = 0;

        for (let j = i; j < s.length; j++) {
            if (!charSet.has(s[j])) {
                charSet.add(s[j]);
                currentLength++;
                maxLength = Math.max(maxLength, currentLength);
            } else {
                break; // A repeating character, so stop and move to the next i.
            }
        }
    }

    return maxLength;
};
```

```js
//o(n) //o(m)
var lengthOfLongestSubstring = function (s) {

  if (s.length === 0 || s === "") return 0;

  maxLength = 1;
  let left = 0;
  let mySet = new Set();

  for (let right = 0; right < s.length; right++) {
    let char = s[right];

    if (mySet.has(char)) {

      while (s[left] !== char) {
        mySet.delete(s[left]);
        console.log(mySet);
        left++;
      }
      left++;
    } else {
      mySet.add(char);
      maxLength = Math.max(maxLength, mySet.size);
    }
  }

  return maxLength;
};

const inputStr = "abcabcbb";
console.log(lengthOfLongestSubstring(inputStr));
```
