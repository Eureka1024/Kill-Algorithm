题目来自于 leetcode 的 [[1929. 数组串联](https://leetcode-cn.com/problems/concatenation-of-array/)](https://leetcode-cn.com/problems/sqrtx/)。

超级简单，找信心的题目。

#### 我的解法

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* getConcatenation(int* nums, int numsSize, int* returnSize){
    int* returnArr = (int*)malloc(sizeof(int)*numsSize*2);

    *returnSize = numsSize * 2;

    for (int i=0; i<numsSize; i++)
    {
        returnArr[i] = nums[i];
        returnArr[i+numsSize] = nums[i];
    }

    return returnArr;
}
```

