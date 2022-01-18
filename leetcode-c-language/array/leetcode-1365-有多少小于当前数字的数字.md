题目来自于 leetcode 的[1365. 有多少小于当前数字的数字](https://leetcode-cn.com/problems/how-many-numbers-are-smaller-than-the-current-number/)。

#### 我的解法

首先想到使用暴力破解，思路很简单，就是效率比较低。

然后想到排序后，比较即可。

由于看到数组元素都比较小，就想到了计数排序，这个排序真滴巧妙，充分利用了数组元素能够随机存储的优点。

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* smallerNumbersThanCurrent(int* nums, int numsSize, int* returnSize){
    int* returnArr = (int*)malloc(sizeof(int)*numsSize);
    int a[101] = {0};
    int sum = 0;
    int buf = 0;

    for (int i = 0; i < numsSize; i++)
    {
        a[nums[i]]++;
    }

    //得到小于每个数的数量
    for (int i = 0; i < 101; i++)
    {
        buf = a[i];
        a[i] = sum;
        sum += buf; 
    }

    for (int i = 0; i < numsSize; i++)
    {
        returnArr[i] = a[nums[i]];
    }

    *returnSize = numsSize;

    return returnArr;
}
```

