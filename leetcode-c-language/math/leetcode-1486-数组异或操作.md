题目来自于 leetcode 的[1486. 数组异或操作](https://leetcode-cn.com/problems/xor-operation-in-an-array/)。



#### 我的解法

就是题目即是答案，就是要注意用于异或的值要初始化为0，因为任何数异或即为其自身。

```c
int xorOperation(int n, int start){
    int xorValue = 0;
    for (int i = 0; i < n; i++)
    {
        xorValue ^= start + 2 * i;
    }

    return xorValue;
}
```

