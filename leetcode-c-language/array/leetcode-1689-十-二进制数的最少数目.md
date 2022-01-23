题目来自于 leetcode 的[1689. 十-二进制数的最少数目](https://leetcode-cn.com/problems/partitioning-into-minimum-number-of-deci-binary-numbers/)。

算是脑筋急转弯，不是很难。

#### 我的解法

主要要注意到只需要找到最大的那个字符即可。

值得注意的是：需要考虑 ASCII 码的转换。

```c
int minPartitions(char * n){
    int maxValue = n[0];

    int i = 1;
    while (n[i] != '\0')
    {
        if (n[i] > maxValue) 
        {
            maxValue = n[i];
        }
        i++;
    }

    return maxValue - '0'; //ASICC码转换成数字
}
```

