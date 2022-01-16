题目来自于 leetcode 的 [27. 移除元素](https://leetcode-cn.com/problems/remove-element/)。

使用双指针的解法即可，就是使用一个变量来记录此时有效的值的位置。

以下是验证过的源码：

```c
int removeElement(int* nums, int numsSize, int val){
    int re_size = 0;

    for(int i=0; i<numsSize; i++)
    {
        if(nums[i] != val)
        {
            nums[re_size++] = nums[i];
        }
    }

    return re_size;
}
```

其实看到顺序可以改变这个提示，我就想到是否会有更优化的功能，后面想想双指针也可以从两侧开始，将后面满足条件的值替换目标的值即可。

最后 left 的值就是最后数组的大小，为什么选择 left，自己画图就知道了。

代码如下：

```c
int removeElement(int* nums, int numsSize, int val){
    int left = 0;
    int right = numsSize - 1;
    
    while (left <= right)
    {
        if(nums[left] == val)
        {
            nums[left] = nums[right];
            right--;
        }
        else
        {
            left++;
        }
    }

    return left;
}
```

