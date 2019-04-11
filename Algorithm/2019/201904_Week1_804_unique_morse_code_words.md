
## Unique Morse Code Words

International Morse Code defines a standard encoding where each letter is mapped to a series of dots and dashes, as follows: "a" maps to ".-", "b" maps to "-...", "c" maps to "-.-.", and so on.

For convenience, the full table for the 26 letters of the English alphabet is given below:

```
[".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."]
```
Now, given a list of words, each word can be written as a concatenation of the Morse code of each letter. For example, "cba" can be written as "-.-..--...", (which is the concatenation "-.-." + "-..." + ".-"). We'll call such a concatenation, the transformation of a word.

Return the number of different transformations among all words we have.
```
Example:
Input: words = ["gin", "zen", "gig", "msg"]
Output: 2
Explanation: 
The transformation of each word is:
"gin" -> "--...-."
"zen" -> "--...-."
"gig" -> "--...--."
"msg" -> "--...--."
```
There are 2 different transformations, "--...-." and "--...--.".

Note:

* The length of words will be at most 100.
* Each words[i] will have length in range [1, 12].
* words[i] will only consist of lowercase letters.

## 解题思路

1. 对字符串数组进行转换，将各字符串转换为莫斯码
2. 对转换的莫斯码数组进行去重计算数量

## 代码

### 使用数组去重统计方法

```javascript
/**
 * @param {string[]} words
 * @return {number}
 */
var uniqueMorseRepresentations = function(words) {
    const MORSE = [".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."];
    const BASE = 'a'.charCodeAt(0);
    let transformed = words.map((val) => {
        let morseWd = '';
        for (let i = 0; i < val.length; i++) {
            let index = val.charCodeAt(i) - BASE;
            morseWd += MORSE[index];
        }
        
        return morseWd;
    });
    
    return new Set(transformed).size;
};
```

### 使用对象的键进行统计

```javascript
/**
 * @param {string[]} words
 * @return {number}
 */
var uniqueMorseRepresentations = function(words) {
    const morse = [".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."];
    const map = {};
    words.forEach(w=>{
        let morseCode = '';
        for(let i = 0; i < w.length; i++) {
            morseCode += morse[w.charCodeAt(i) - 97];
        }
        map[morseCode] = null;
    });
    
    return Object.keys(map).length;
};
```

### 使用ES6中的Set进行统计

```javascript
/**
 * @param {string[]} words
 * @return {number}
 */
var uniqueMorseRepresentations = function(words) {
        var alphabet = [".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."];
        var results = new Set();
        words.forEach(function(w){
            let result = ""
            for (let i = 0; i < w.length; i ++) {
                result += alphabet[w.charCodeAt(i) - 97]
            }
            results.add(result)
        })
        return results.size;
};
```

### 使用Set和数组Reduce方法进行统计

```javascript
/**
 * @param {string[]} words
 * @return {number}
 */
var uniqueMorseRepresentations = function (words) {
  const map = { a: '.-', b: '-...', c: '-.-.', d: '-..', e: '.', f: '..-.', g: '--.', h: '....', i: '..', j: '.---', k: '-.-', l: '.-..', m: '--', n: '-.', o: '---', p: '.--.', q: '--.-', r: '.-.', s: '...', t: '-', u: '..-', v: '...-', w: '.--', x: '-..-', y: '-.--', z: '--..' }
  return new Set(words.map(val => Array.prototype.reduce.call(val, (total, letter) => total + map[letter], ''))).size
}
```

## 关于数组去重的思考


数组去重的一些参考文章

* [JavaScript专题之数组去重](https://github.com/mqyqingfeng/Blog/issues/27)
