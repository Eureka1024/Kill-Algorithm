题目来自于 leetcode 的 [35. 搜索插入位置](https://leetcode-cn.com/problems/search-insert-position/)。

解法：其实就是二分查找的稍微变种，若最后查找未果，返回 `right+1`即可，因为如果最后找不到，说明搜索范围的 right 已经小于且最接近目标值。

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

    return right+1;
    //return left; //这个等效
}
```

