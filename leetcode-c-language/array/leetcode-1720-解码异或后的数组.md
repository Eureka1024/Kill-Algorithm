题目来自于 leetcode 的[[1720. 解码异或后的数组](https://leetcode-cn.com/problems/decode-xored-array/)](https://leetcode-cn.com/problems/final-value-of-variable-after-performing-operations/)。

题目难度一般吧。

#### 我的解法

关键点是明白这个关系 

a^b = c  =>  a=b^c

结果就出来了

推导过程看这篇文章：https://leetcode-cn.com/problems/decode-xored-array/solution/jie-ma-yi-huo-hou-de-shu-zu-by-leetcode-yp0mg/

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* decode(int* encoded, int encodedSize, int first, int* returnSize){
    int* returnVal = (int*)malloc(sizeof(int)*(encodedSize+1));

    *returnSize = encodedSize+1;

    returnVal[0] = first;

    for (int i=0; i<encodedSize; i++)
    {
        returnVal[i+1] = returnVal[i] ^ encoded[i];
    }

    return returnVal;
}
```

