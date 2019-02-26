
问题：
输入一个数，判断是否为质数(质数为除了1和本身，不能被其他数整除的正整数)

解决方案:

思路：主要是判断是否能被中间的数整除，缩小查找的范围，可以提高效率。

```javascript
    function isPrimeNum(num) {
      for (let i = 2; i < num; i++) {
        if (num%i === 0) {
          return false;
        }
      }

      return true;
    }

    function isPrimeNum1(num) {
      for (let i = 2; i < num/2+1; i++) {
        if (num%i === 0) {
          return false;
        }
      }

      return true;
    }

    function isPrimeNum2(num) {
      if (typeof num !== 'number' || !Number.isInteger(num)) {
        return false;
      }
      for (let i = 2; i <= Math.sqrt(num); i++) {
        if (num%i === 0) {
          return false;
        }
      }

      return true;
    }

    function isPrimeNum3(num) {
      return !/^1?$|^(11+?)\1+$/.test(Array(num + 1).join('1'));
    }
```