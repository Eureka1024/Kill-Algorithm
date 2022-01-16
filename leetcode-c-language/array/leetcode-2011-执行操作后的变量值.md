题目来自于 leetcode 的[2011. 执行操作后的变量值](https://leetcode-cn.com/problems/final-value-of-variable-after-performing-operations/)。

超级简单，找信心的题目。

#### 我的解法

看到关键：只需要判断三个字母中间的字母即可。

```c
int finalValueAfterOperations(char ** operations, int operationsSize){
    int value = 0;

    for (int i=0; i<operationsSize; i++)
    {
        if (operations[i][1] == '+')
        {
            value++;
        }
        else
        {
            value--;
        }
    }

    return value;
}
```

