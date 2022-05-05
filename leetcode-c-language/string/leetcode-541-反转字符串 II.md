题目来自于 leetcode 的 [541. 反转字符串 II](https://leetcode-cn.com/problems/reverse-string-ii/)。



#### 我的解法

比较好的方式就是利用 `i += (2*k)` 来跳转满足的范围，最后实现翻转数据的统一。

```c
char * reverseStr(char * s, int k){
    int len = strlen(s);

    for (int i = 0; i < len; i += (2*k))
    {
        if ((len - i) <= k)
        {
            k = len - i;//最后的一组数据缩小k的范围方便翻转
        }

        int left = i;
        int right = i + k - 1;
        int temp = 0; 
        while (left < right)
        {
            temp = s[left];
            s[left++] = s[right];
            s[right--] = temp;
        }
    }

    return s;
}
```

