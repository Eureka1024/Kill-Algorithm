题目来自于 leetcode 的 [34. 在排序数组中查找元素的第一个和最后一个位置](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)。

解决此题思路：

该题其实就是二分查找的变种，就是存在多个目标值，求两边的位置。

刚开始陷入麻烦的是自己想要得到一个简短的实现就能找到边界，结果陷入了构建一个麻烦的判断解法，后来想想，简单点不就好了。

所以就将问题分解，一个个边界的求，结果就很简单了，直接上代码：

以下是验证过的源码：

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* searchRange(int* nums, int numsSize, int target, int* returnSize){

    int* re = (int*)malloc(2*sizeof(int));
    int left = 0;
    int right = numsSize - 1;
    int mid;
    *returnSize = 2;

    if(nums == NULL)
    {
        re[0] = -1;
        re[1] = -1;
    }
	
    //先找到其中一个值，若没有可直接按要求返回
    while(left <= right)
    {
        mid = ((right-left)>>1) + left;

        if (nums[mid] > target)
        {
            right = mid - 1;
        }
        else if (nums[mid] < target)
        {
            left = mid + 1;
        }
        else 
        {
           break;
        }
    }

    //若没有目标值，按要求返回
    if(left > right)
    {
        re[0] = -1;
        re[1] = -1;
        return re;
    }

    //查找左边界
    left = 0;
    right = mid;
    while(left <= right)
    {
        mid = ((right-left)>>1) + left;

        if (nums[mid] < target)
        {
            left = mid + 1;
        }
        else if (nums[mid] == target)
        {
            if((mid == 0) || (nums[mid-1] != target))
            {
                re[0] = mid;
                break;
            }

            right = mid - 1;
        }
    }

    //查找右边界
    left = mid;
    right = numsSize - 1;
    while(left <= right)
    {
        mid = ((right-left)>>1) + left;

        if (nums[mid] > target)
        {
            right = mid - 1;
        }
        else if (nums[mid] == target)
        {
            if((mid == numsSize-1) || (nums[mid+1] != target))
            {
                re[1] = mid;
                break;
            }

            left = mid + 1;
        }
    }

    return re;
}
```

