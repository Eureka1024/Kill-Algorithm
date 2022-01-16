题目来自于 leetcode 的 [[66. 加一](https://leetcode-cn.com/problems/plus-one/)](https://leetcode-cn.com/problems/sqrtx/)。

就是普通的简单题而已。

#### 我的解法

就是要注意是否需要额外增加一个数组元素即可。

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* plusOne(int* digits, int digitsSize, int* returnSize){
    int carry = 1;
    int* returnArr = NULL;
    for (int i=digitsSize-1; i>=0; i--)
    {
        if ((digits[i] == 9) && (carry == 1))
        {
            digits[i] = 0;
            carry = 1;
        }
        else
        {
            digits[i] += 1;
            carry = 0;
            break;
        }
    }

    if (carry == 1) 
        *returnSize = digitsSize + 1;
    else 
        *returnSize = digitsSize;

    returnArr = (int*)malloc(sizeof(int)*(*returnSize));

    if (carry == 1)  returnArr[0] = 1;
    
    for(int i=0; i<digitsSize; i++)
    {
       returnArr[i+carry] = digits[i];
    }

    return returnArr;
}
```

