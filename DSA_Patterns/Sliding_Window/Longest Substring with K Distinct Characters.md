Longest Substring with K Distinct Characters
- const inputStr = "aabbcccdeefff";
- const k = 3;


```js
function longestSubstrWithKUniqueChars(inputStr, k) {
  if (k <= 0 || k > inputStr.length) {
    return "Invalid input";
  }

  let longestSubstr = [];
  let maxLength = 0

  for (let i = 0; i < inputStr.length; i++) {
    for (let j = i + 1; j <= inputStr.length; j++) {
      const substring = inputStr.slice(i, j);
      const uniqueChars = new Set(substring);

      if (uniqueChars.size === k && substring.length > longestSubstr.length) {
        longestSubstr.push([substring]);
        maxLength = Math.max(maxLength, substring.length)
      }
    }
  }
  console.log(longestSubstr);
  return maxLength;
}

// Example usage:
const inputStr = "aabbcccdeefff";
const k = 3;
console.log(longestSubstrWithKUniqueChars(inputStr, k)); // Output: "cccdee"
```

```js
//Optimised - restudy
// O(n)
//o(n)
function longestSubstrWithKUniqueChars(inputStr, k) {
  if (k <= 0 || k > inputStr.length) {
    return "Invalid input";
  }

  let left = 0;
  let maxLength = 0;
  let maxSubstring = "";
  const charCount = new Map();

  for (let right = 0; right < inputStr.length; right++) {
    const char = inputStr[right];

    charCount.set(char, (charCount.get(char) || 0) + 1);

    while (charCount.size > k) {
      const startChar = inputStr[left];
      charCount.set(startChar, charCount.get(startChar) - 1);
      if (charCount.get(startChar) === 0) {
        charCount.delete(startChar);
      }
      left++;
    }

    if (right - left + 1 > maxLength) {
      maxLength = right - left + 1;
      maxSubstring = inputStr.slice(left, right + 1);
    }
  }

  return [maxSubstring, maxLength];
}

// Example usage:
const inputStr = "aabbcccdeefff";
const k = 3;
console.log(longestSubstrWithKUniqueChars(inputStr, k)); // Output: "aabbccc"
```
