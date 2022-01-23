题目来自于 leetcode 的[[1281. 整数的各位积和之差](https://leetcode-cn.com/problems/subtract-the-product-and-sum-of-digits-of-an-integer/)](https://leetcode-cn.com/problems/final-value-of-variable-after-performing-operations/)。

不算难的题目，就一点点技巧。

#### 我的解法

通过对十取余获得最低位的数字，通过对十作除法消掉最低位。

```c
int subtractProductAndSum(int n){
    int sum = 0;
    int product = 1;
    int i;
    while (n > 0)
    {
        i = n % 10;
        sum += i;
        product *= i;

        n = n / 10;
    }

    return product - sum;
}
```

