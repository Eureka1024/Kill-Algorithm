题目来自于 leetcode 的 [1920. 基于排列构建数组](https://leetcode-cn.com/problems/build-array-from-permutation/)

就是普通的简单题而已。

#### 我的解法

其实题目就是解法。

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* buildArray(int* nums, int numsSize, int* returnSize){
    int* returnNums = (int*)malloc(sizeof(int)*numsSize);

    for (int i = 0; i < numsSize; i++)
    {
        returnNums[i] = nums[nums[i]];
    }

    *returnSize = numsSize;

    return returnNums;
}
```

## 参考

官方题解除了提供跟我类似的解法，还有一种可以在空间复杂度为 O(1)的条件下的实现：依赖于题目的提示：

> **提示：**
>
> - `1 <= nums.length <= 1000`
> - `0 <= nums[i] < nums.length`
> - `nums` 中的元素 **互不相同**

可以利用整形数大于1000的部分来存储结果，之后再获得最终的结果。

[官方题解 - 基于排列构建数组](https://leetcode-cn.com/problems/build-array-from-permutation/solution/ji-yu-pai-lie-gou-jian-shu-zu-by-leetcod-gjcn/)

