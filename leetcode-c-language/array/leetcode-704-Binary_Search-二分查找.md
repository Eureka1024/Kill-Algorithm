题目来自于 leetcode 的 [704. 二分查找](https://leetcode-cn.com/problems/binary-search/)。

解决此题需要注意：

- 终止条件为 `left <= right`，一定要把范围覆盖完

- 避免溢出，选择 `mid = (right-left)/2`，而不是 `mid = (right+left)/2`

- 缩减范围时，要有效的更新，`right = mid - 1;`，而不是 `right = mid`，否则可能会造成死循环。

- 如果考虑到运行效率，考虑使用移位 `>>1` 代替除法 `/2`。

  注意移位运算法优先级低于算数运算符。

以下是验证过的源码：

```c
int search(int* nums, int numsSize, int target){
    int left = 0;
    int right = numsSize - 1;
    int mid;

    while(left <= right)
    {
        mid = ((right-left)>>1) + left;

        if (nums[mid] > target)
        {
            right = mid - 1;
        }
        else if(nums[mid] < target)
        {
            left = mid + 1;
        }
        else
        {
            return mid;
        }
    }

    return -1;
}
```

