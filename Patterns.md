# Paterns - NESTED LOOPS
## 4 Rules:
    1. count the number of lines for the outer loop
    2. for the inner loop focus on the column and somehow connect to the row
    3. print char in inner for loop.
    4. observe the symmetry {optional}

```js
//print
// ****
// ****
// ****
// ****
const printPattern1 = (n) => {
    let pattern = '';
    for (let i = 0; i < n; i++) {
        for (let j = 0; j < n; j++) {
            pattern = pattern + '*';
        }
        pattern = pattern + "\n";
    }
    return pattern;
}
```
```js
//print
// *
// **
// ***
// ****
const printPattern2 = (n) => {
    let pattern = '';
    for (let i = 0; i < n; i++) {
        for (let j = 0; j <= i; j++) {
            pattern += char;
        }
        pattern += '\n';
    }
    return pattern;
}
```
```js
//print
// 1
// 12
// 123
// 1234
const printPattern3 = (n) => {
    var pattern = 0;
    for (let i = 1; i <= n; i++) {
        for (let j = 1; j <= i; j++) {
            pattern = pattern + j;
        }
        pattern += '\n';
    }
    return pattern;
}
```
```js
//print
// 1
// 22
// 333
// 4444

const printPattern4 = (n) => {
    let pattern = 0;
    for (let i = 1; i <= n; i++) {
        for (let j = 1; j <= i; j++) {
            pattern += i;
        }
        pattern += '\n';
    }
    return pattern;
}
```
```js
//print
// ****
// ***
// **
// *

const printPattern5 = (n) => {
    let pattern = '';
    for (let i = 1; i <= n; i++) {
        for (let j = n; j >= i; j--) {
            pattern += '*';
        }
        pattern += '\n';
    }
    return pattern;
}
```
```js
//print
// 1234
// 123
// 12
// 1

const printPattern6 = (n) => {
    let pattern = '';
    for (let i = 0; i < n; i++) {
        for (let j = 1; j < (n - i) + 1; j++) {
            pattern += j;
        }
        pattern += '\n';
    }
    return pattern;
}
console.log(printPattern6(5));
```
```js
//print
//  0        *      [3, 1 , 3] n-i-1, 2*i+1  ,n-i-1
//  1       ***     [2, 3 , 2] n-i-1, 2*i+1  ,n-i-1
//  2      *****    [1, 5 , 1] n-i-1, 2*i+1  ,n-i-1
//  3     *******   [0, 7 , 0] n-i-1, 2*i+1  ,n-i-1

const printPattern7 = (n) => {
    let pattern = '';
    for (i = 0; i < n; i++) {
        //space
        for (let j = 0; j < n - i - 1; j++) {
            pattern += ' '
        }
        //star
        for (let j = 0; j < 2 * i + 1; j++) {
            pattern += '*';
        }

        //space
        for (let j = 0; j < n - i - 1; j++) {
            pattern += ' '
        }
        pattern += '\n';
    }
    return pattern;
}
```
```js
//print
//  0     *******   [0, 7 , 0] i,  2*n - 2*i+1   ,i
//  1      *****    [1, 5 , 1] i,  2*n - 2*i+1   ,i
//  2       ***     [2, 3 , 2] i,  2*n - 2*i+1   ,i
//  3        *      [3, 1 , 3] i,  2*n - 2*i+1   ,i
const printPattern8 = (n) => {
    let pattern = '';
    for (i = 0; i < n; i++) {
        //space
        for (let j = 0; j < i; j++) {
            pattern += ' '
        }
        //star
        for (let j = 0; j < (2 * n) - (2 * i + 1); j++) {
            pattern += '*';
        }

        //space
        for (let j = 0; j < i; j++) {
            pattern += ' '
        }
        pattern += '\n';
    }
    return pattern;
}
```
```js
//print
//     *
//    ***
//   *****
//  *******
// *********
// *********
//  *******
//   *****
//    ***
//     *
const printPattern9 = (n) => {
    console.log(printPattern7(n));
    console.log(printPattern8(n));
}
```
```js
//print
// 1 * 
// 2 ** 2 * n - 1
// 3 ***
// 4 ****
// 5 ***
// 6 **
// 7 *

const printPattern10 = (n) => {
    let pattern = '';
    for (let i = 1; i <= 2 * n - 1; i++) {
        var stars = i;
        if (i > n) stars = 2 * n - i;
        for (let j = 1; j <= stars; j++) {
            pattern += '*';
        }
        pattern += '\n';
    }
    return pattern;
}
```
```js
//print
// 1
// 01
// 101
// 0101
// 10101

const printPattern11 = (n) => {
    let pattern = '';
    for (let i = 0; i <= n; i++) {
        var start = (i % 2 == 0) ? 1 : 0;
        for (let j = 0; j <= i; j++) {
            pattern += start;
            start = 1 - start;
        }
        pattern += '\n';
    }
    return pattern;
}
```
```js
//print
// 1      1
// 12    21
// 123  321
// 12344321
const printPattern12 = (n) => {
    var pattern = '';
    var space = 2 * (n - 1);
    for (let i = 1; i <= n; i++) {
        //number
        for (let j = 1; j <= i; j++) {
            pattern += j;
        }

        //space
        for (let j = 1; j <= space; j++) {
            pattern += ' ';
        }

        //number
        for (let j = i; j >= 1; j--) {
            pattern += j;
        }
        space = space - 2;
        pattern += '\n';
    }
    return pattern;
}
```
