题目来自于 leetcode 的[1512. 好数对的数目](https://leetcode-cn.com/problems/number-of-good-pairs/)。

暴力破解，永远滴神。

#### 我的解法

这种题很容易想到暴力破解，简单好用，缺点就是不高效。

```c
int numIdenticalPairs(int* nums, int numsSize){
    int goodNums = 0;

    for (int i = 0; i < numsSize; i++)
    {
        for (int j = i+1; j < numsSize; j++)
        {
            if (nums[i] == nums[j]) goodNums++;
        }
    }

    return goodNums;
}
```

#### 他山之石

题解中的哈希表其实没怎么看懂，但是看到评论区中的利用桶排序类似的思想，可以实现快速地得到结果，将时间复杂度从 O(n^2) 变成 O(n)。

值得说明的是，arr[i] 存的是当增加一个数多出的对数，比如如果是第四个相同的数，则应该将结果加3，这个桶装的值真是恰到好处。

```c
int numIdenticalPairs(int* nums, int numsSize){
    int goodNums = 0;

    int arr[101] = {0};

    for (int i = 0; i < numsSize; i++)
    {
        goodNums += arr[nums[i]];
        arr[nums[i]]++;
    }

    return goodNums;
}
```

