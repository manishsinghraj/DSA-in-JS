# Fruit Into Baskets

## Problem Statement

You are visiting a farm that has a single row of fruit trees arranged from left to right. The trees are represented by an integer array `fruits` where `fruits[i]` is the type of fruit the `i`th tree produces.

You want to collect as much fruit as possible. However, the owner has some strict rules that you must follow:

- You only have two baskets, and each basket can only hold a single type of fruit. There is no limit on the amount of fruit each basket can hold.
- Starting from any tree of your choice, you must pick exactly one fruit from every tree (including the start tree) while moving to the right. The picked fruits must fit in one of your baskets.
- Once you reach a tree with fruit that cannot fit in your baskets, you must stop.

Given the integer array `fruits`, return the maximum number of fruits you can pick.
<br>
## Example:
<br>
- Input: fruits = [1,2,1]
- Output: 3
- Explanation: We can pick from all 3 trees.
<br>
- Input: fruits = [0,1,2,2]
- Output: 3
- Explanation: We can pick from trees [1,2,2].
- If we had started at the first tree, we would only pick from trees [0,1].
<br>

- Input: fruits = [1,2,3,2,2]
- Output: 4
- Explanation: We can pick from trees [2,3,2,2].
- If we had started at the first tree, we would only pick from trees [1,2].

<br>
- Constraints:

- 1 <= fruits.length <= 105
- 0 <= fruits[i] < fruits.length


```js
/**
 * @param {number[]} fruits
 * @return {number}
 */

//Time limit exceeded
 //o(n^2) //o(n)
var totalFruit = function (fruits) {
  if (!fruits || !fruits.length) return 0;

  let maxLength = 0;

  for (let i = 0; i < fruits.length; i++) {
    let fruitSet = new Set();
    let uniqueFruitsCount = 0;

    for (let j = i; j < fruits.length; j++) {
      const fruit = fruits[j];
      fruitSet.add(fruit);

      if (fruitSet.size > 2) {
        break;
      }

      if (fruitSet.size <= 2) {
        uniqueFruitsCount = j - i + 1;
        maxLength = Math.max(maxLength, uniqueFruitsCount);
      }
    }
  }

  return maxLength;
};

// Example usage:
const inputStr = [1, 2, 1, 1, 3, 4, 2, 2, 2, 2, 4];
console.log(totalFruit(inputStr));
```
```js
//o(n) //o(m)

/**
 * @param {number[]} fruits
 * @return {number}
 */

 //o(n^3) //o(n)
var totalFruit = function(fruits) {
    if (!fruits || !fruits.length) return 0;

    let maxFruitCount = 0;
    let left = 0;
    let uniqueFruitBasket = new Map();

    for(let right = 0; right < fruits.length; right++){
        let fruit = fruits[right];
        uniqueFruitBasket.set(fruit, (uniqueFruitBasket.get(fruit) || 0) + 1 );

        while(uniqueFruitBasket.size > 2){
            //remove the left element from basket and increment the pointer left
            let removedFruit = fruits[left];
            uniqueFruitBasket.set(removedFruit, (uniqueFruitBasket.get(removedFruit) || 0) - 1);

            if(uniqueFruitBasket.get(removedFruit) === 0){
                uniqueFruitBasket.delete(removedFruit);
            }
            left++;
        }

        maxFruitCount = Math.max(maxFruitCount, right - left + 1);
    }

return maxFruitCount;
};
```  
