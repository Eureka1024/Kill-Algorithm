题目来自于 leetcode 的[[59. 螺旋矩阵 II](https://leetcode-cn.com/problems/spiral-matrix-ii/)](https://leetcode-cn.com/problems/final-value-of-variable-after-performing-operations/)。

题目不简单，找到方法就不难。

#### 我的解法

重要的是**循环不变量原则**，找到一个规律，在旋转的时候保持一些不变的东西。

```c
/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
int** generateMatrix(int n, int* returnSize, int** returnColumnSizes){
    
    *returnSize = n;//返回n行
    *returnColumnSizes = (int*)malloc(sizeof(int)*n);//记录n行有多少列

    int** returnMatrix = (int**)malloc(sizeof(int*)*n);//n行（数组指针）

    for (int i = 0; i < n; i++)
    {
        returnMatrix[i] = (int*)malloc(sizeof(int)*n);//每一行的元素个数
        (*returnColumnSizes)[i] = n;
    }

    int currentN = n;
    int initRow = 0;
    int initColumn = 0;
    int initNum = 1;//初始化参数

    if (currentN == 1)
    {
        returnMatrix[0][0] = 1;
    }

    while (currentN > 1)
    {
        //从左到右
        for (int i = 0; i < (currentN-1); i++)
        {
            returnMatrix[initRow][initColumn] = initNum++;
            initColumn += 1;
        }
    
        //从上到下
        for (int i = 0; i < (currentN-1); i++)
        {
            returnMatrix[initRow][initColumn] = initNum++;
            initRow += 1;
        }
        
        //从右到左
        for (int i = 0; i < (currentN-1); i++)
        {
            returnMatrix[initRow][initColumn] = initNum++;
            initColumn -= 1;
        }

        //从下到上
        for (int i = 0; i < (currentN-1); i++)
        {
            returnMatrix[initRow][initColumn] = initNum++;
            initRow -= 1;
        }

        currentN -= 2;
        initRow += 1;
        initColumn += 1;
    }

    if (n%2)
    {
        returnMatrix[n/2][n/2] = initNum;
    }
    return returnMatrix;
}
```

