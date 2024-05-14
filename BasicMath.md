### Basic Math

```js
//Count digits for a given number
// n = 23546; //5

const countDigits1 = (n) => {
    var counter = 0;
    while (n > 0) {
        n = Math.floor(n / 10);
        counter++;
    }
    return counter;
}
// Time Complexity: O(log10(n)) or O(num digits)
// Auxiliary Space: O(1) or constant
```
```js

const countDigits2 = (n) => {
    var string = n.toString();
    console.log(string.length);
}
// Time Complexity: O(1) or constant
// Auxiliary Space: O(Number of digits in an integer)
```
```js
// Log - based Solution to count digits in an integer
// We can use log10(logarithm of base 10) to count the number of digits of positive numbers(logarithm is not defined for negative numbers).
// Digit count of N = upper bound of log10(N).

const countDigits3 = (n) => {
    return Math.floor(Math.log10(n) + 1);
}
// Time Complexity: O(1) or constant
// Auxiliary Space: O(1) or constant
```
```js
// Problem Statement: Given a number N reverse the number and print it.
// Example 1:
// Input: N = 123
// Output: 321
// Explanation: The reverse of 123 is 321

// Example 2:
// Input: N = 234
// Output: 432
// Explanation: The reverse of 234 is 432

const reverseANumber = (n) => {
    var reversedNumber = 0;
    while (n !== 0) {
        reversedNumber = (n % 10) + (reversedNumber * 10);
        n = Math.floor(n / 10);
    }
    return reversedNumber;
}

```
```js
//Palindrome

const isPalindrome = (n) => {
    var reversedNumb = 0;
    var givenNum = n;
    while (n !== 0) {
        reversedNumb = (reversedNumb * 10) + (n % 10);
        n = Math.floor(n / 10);
    }
    if (reversedNumb == givenNum) return true
    else return false;

}

console.log(palindrome(121));

const palindrome = (str) => {
    let givenStr = str;
    let reversedStr = '';

    for(let i = str.length -1; i >=0; i--){
        reversedStr += str[i];
    }

    return reversedStr === givenStr;
}

console.log(palindrome("mAm"));


const isPalindrome = (input) => {
    // Convert input to string if it's a number
    const str = typeof input === 'number' ? String(input) : input;

    // Reverse the string
    const reversedStr = str.split('').reverse().join('');

    // Check if the original string is equal to the reversed string
    return str === reversedStr;
}

console.log(isPalindrome(121)); // true (number)
console.log(isPalindrome("12s1")); // true (string)

```

```js
//Armstongs number
//123 => 1^3 + 2^3 + 3^3 = if it gives 123, then its armstrong
// sum = 0;
// 123 % 10 => 3 * 3 * 3
// 123 / 10 = 12 => 12 % 10 => 2 * 2 * 2
// sum = sum + ld

// Armstrong Numbers
// 1, 2, 3, 4, 5, 6, 7, 8, 9, 153

const isArmstrong = (n) => {
    var sum = 0;
    var givenNum = n;
    var noOfDigits = n.toString().length;
    while (n !== 0) {
        var lastDigit = n % 10;
        sum = sum + Math.pow(lastDigit, noOfDigits); //OR  lastDigit ** noOfDigits
        n = Math.floor(n / 10);
    }
    console.log(sum)
    if (sum == givenNum) {
        return console.log("Is Armstrong");
    } else {
        return console.log("Not an Armstrong");
    }
}

```

```js
//Print all divisors

//36-> 1,2,3,4,6,9,12,18,36

const printAllDivisor1 = (n) => {
    let divisors = [];
    for (let i = 1; i <= n; i++) {
        if (n % i == 0) {
            divisors.push(i);
        }
    }
    return divisors;
}
```

```js
const printAllDivisor2 = (n) => {
    let divisors = [];
    for (let i = 1; i <= Math.sqrt(n); i++) { //for (let i = 1; i*i <= n; i++) {
        if (n % i == 0) {
            divisors.push(i);
            if (Math.floor(n / i) !== i) {
                divisors.push(n / i);
            }
        }

    }
    console.log(divisors);
    return divisors.sort(function (a, b) { return a - b }); 
    //https://forum.freecodecamp.org/t/arr-sort-a-b-a-b-explanation/167677/13
    //quicksort?
}
```

```js
//Prime Number
//number which has 2 factors 1 and itself
// 11 - 1 & 11 - Prime
// 3 - 1 & 3 - Prime
// 4 - 1, 2, 4 - Not Prime 


// we can add counter and if it is 2, then its prime number.

const isPrime1 = (n) => {
    var count = 0;
    for (let i = 1; i <= n; i++) {
        if (n % i == 0) {
            count++;
        }
    }
    console.log(count)
    if (count == 2) {
        return true;
    } else {
        return false;
    }
}
//TC - O(N)
```

```js

// tofind factors of number, looping till sqrt of number is enough.
// for loop till sqrt of n
// check if (n)

const isPrime2 = (n) => {
    var count = 0;
    for (let i = 1; i * i <= n; i++) {
        if (n % i == 0) {
            count++;
            if (Math.floor(n % i) !== i) {
                count++;
            }
        }
    }
    console.log(count)
    if (count == 2) {
        return true;
    } else {
        return false;
    }

}
//TC - O(N)


const isPrime3 = (n) => {
    if (n <= 1) {
        return false; // 0 and 1 are not prime numbers
    }
    for (let i = 2; i <= Math.sqrt(n); i++) {
        if (n % i === 0) {
            return false; // If n is divisible by any number less than or equal to its square root, it's not prime
        }
    }
    return true; // If no divisors are found, n is prime
}

console.log(isPrime3(2)); // Output: false
```

```js
//Find GCD of given numbers

const findGCD1 = (a, b) => {
    var gcd = 1;
    for (let i = 1; i <= Math.min(a, b); i++) {
        if (a % i == 0 && b % i == 0) {
            gcd = i;
        }
    }
    return gcd;
}

//Using Euclidean algorithm
const findGCD3 = (a, b) => {

    while (a > 0 && b > 0) {
        if (a > b) a = a % b;
        if (b > a) b = b % a;

        if (a == 0) return b;
        return a;
    }
}
```
