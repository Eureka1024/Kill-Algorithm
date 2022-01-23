题目来自于 leetcode 的[1431. 拥有最多糖果的孩子](https://leetcode-cn.com/problems/kids-with-the-greatest-number-of-candies/)

挺简单的，找信心。

#### 我的解法

找最大值，然后给每个孩子的糖果增加额外的糖果后，与之判断即可。

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
bool* kidsWithCandies(int* candies, int candiesSize, int extraCandies, int* returnSize){
    bool* returnArr = (bool*)malloc(sizeof(bool) * candiesSize);
    int max = candies[0];
    for (int i = 1; i < candiesSize; i++)
    {
        if(candies[i] > max) max = candies[i];
    }

    for (int i = 0; i < candiesSize; i++)
    {
        if((candies[i] + extraCandies) >= max)
        {
            returnArr[i] = true;
        }
        else
        {
            returnArr[i] = false;
        }
    }

    *returnSize = candiesSize;
    return returnArr;
}
```

