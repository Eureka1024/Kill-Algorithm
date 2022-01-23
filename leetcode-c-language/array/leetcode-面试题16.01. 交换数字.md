题目来自于 leetcode 的[[面试题 16.01. 交换数字](https://leetcode-cn.com/problems/swap-numbers-lcci/)](https://leetcode-cn.com/problems/final-value-of-variable-after-performing-operations/)。

要懂点位运算的性质。

#### 我的解法

根据异或运算的三个性质即可求解：

- 变量与自身异或结果为0
- 变量与0异或结果为自身
- 异或满足结合律

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* swapNumbers(int* numbers, int numbersSize, int* returnSize){
    numbers[0] = numbers[0] ^ numbers[1];
    numbers[1] = numbers[0] ^ numbers[1];
    numbers[0] = numbers[0] ^ numbers[1];

    *returnSize = 2;

    return numbers;
}
```

