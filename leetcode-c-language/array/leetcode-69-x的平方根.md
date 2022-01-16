题目来自于 leetcode 的 [69. x 的平方根](https://leetcode-cn.com/problems/sqrtx/)。

虽说是简单题，还是掉坑了，输在了没有考虑数据溢出的问题。

遇到乘法还是要注意溢出，太容易出现了，检查的时候注意一下最大值最小值之类的临界条件。

#### 我的解法

因为如果 `x` 值是整形中的最大值，其一半的相乘就会溢出。我这里用了不怎么光彩的方法规避，利用电脑求出最大值的平方根，然后将求解范围规避就好了。

但是这样不仅仅是利用了外界计算这种不光彩的方式，还有一个潜在的问题，因为我假设了 int 是 32 位的数据类型，如果平台的 int 是别的字节大小的类型，这种方法就会出错。

以下是我的解法，虽然勉强能通过。

```c
int mySqrt(int x){
    int left = 0;
    int right = 46340;
    int mid;
    int res;
    while(left <= right)
    {
        mid = ((right-left)>>1) + left;
        res =  mid * mid;
        if (res > x)
        {
            right = mid - 1;
        }
        else if(res < x)
        {
            left = mid + 1;
        }
        else
        {
            return mid;
        }
    }

    return right;
}
```

#### 借鉴后的解法

看了官方的题解，果然不愧是官方。

至于解法三中的牛顿迭代，很好的数学方法，可惜我不会，牛顿，yyds。

还是关注使用二分查找实现的吧。

我的题解存在的问题，官方使用类型提升就能解决，提升到最大的整形，芜湖。

下面是我更改后的答案：

```c
int mySqrt(int x){
    int left = 0;
    int right = x;
    int mid;
    long long  res;
    while(left <= right)
    {
        mid = ((right-left)>>1) + left;
        res = (long long)mid * mid;
        if (res > x)
        {
            right = mid - 1;
        }
        else if(res < x)
        {
            left = mid + 1;
        }
        else
        {
            return mid;
        }
    }

    return right;
}
```

