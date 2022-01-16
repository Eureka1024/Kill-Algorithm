题目来自于 leetcode 的 [367. 有效的完全平方数](https://leetcode-cn.com/problems/valid-perfect-square/)。

一旦你会写二分查找，这道题就很简单了。注意一下运算过程中别溢出就好了。

官方题解中的 牛顿迭代解法 很厉害，有空学习学习。

#### 我的解法

```c
bool isPerfectSquare(int num){
    int left = 0;
    int right = num;
    int mid;

    while(left <= right)
    {
        mid = ((right-left)>>1) + left;

        if ((long long)mid*mid > num)
        {
            right = mid - 1;
        }
        else if((long long)mid*mid < num)
        {
            left = mid + 1;
        }
        else
        {
            return true;
        }
    }

    return false;
}
```

