希尔排序基于插入排序进行的改进，先了解插入排序的原理：

## 插入排序

思路：从数组索引第1项开始依次将元素插入到前面的序列中。

代码：

```js
    function sort(array) {
      var len = array.length,i,j,tmp,result;

      result = array.slice(0);
      for (i = 1; i < len; i++) {
        tmp = result[i];
        j = i - 1;
        while(j>=0 && tmp < result[j]) {
          result[j+1] = result[j];
          j--;
        }
        result[j+1] = tmp;
      }

      return result;
    }

    var x = [53,27,36,15,69,42];
    console.log(sort(x));
```

## 希尔排序

思路: 先对若干个子序列进行插入排序，待整个序列基本有序时，再整体进行一次插入排序。(针对希尔排序的思路，排序思路比较难理解)

代码: 
```js
    function sort3(array) {
      var len = array.length, gap = parseInt(len/2),i,j,tmp,result;
      result = array.slice(0);
      while(gap > 0) {
        console.log('gap: ', gap, 'result: ', result);
        for (i = gap; i < len; i++) {
          tmp = result[i];
          j = i - gap;
          while(j >= 0 && tmp < result[j]) {
            result[j + gap] = result[j];
            j = j - gap;
          }
          result[j + gap] = tmp;
        }
        gap = parseInt(gap/2);
      }
      return result;
    }

    var x = [53,27,36,15,69,42];
    console.log(sort3(x));
```