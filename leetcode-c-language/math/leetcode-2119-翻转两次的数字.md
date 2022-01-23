题目来自于 leetcode 的[2119. 反转两次的数字](https://leetcode-cn.com/problems/a-number-after-a-double-reversal/)。

不算难的题目，就一点点技巧。

#### 我的解法

除去为0的特殊情况，判断最后一位是否为0即可。

```c
bool isSameAfterReversals(int num){
    if (num == 0) return true;

    if (num % 10 == 0) return false;

    return true;
}
```

