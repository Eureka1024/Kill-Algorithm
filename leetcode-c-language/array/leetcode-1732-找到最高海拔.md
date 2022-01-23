题目来自于 leetcode 的[[1732. 找到最高海拔](https://leetcode-cn.com/problems/find-the-highest-altitude/)](https://leetcode-cn.com/problems/final-value-of-variable-after-performing-operations/)。

还行。

#### 我的解法

记录每一个点的海拔高度，然后用一个值记录最大值即可。

```c
int largestAltitude(int* gain, int gainSize){

    int gainMax = 0;
    int gainCurrent = 0;

    for (int i = 0; i < gainSize; i++)
    {
        gainCurrent += gain[i];

        if (gainCurrent > gainMax) gainMax = gainCurrent;
    }

    return gainMax;
}
```

