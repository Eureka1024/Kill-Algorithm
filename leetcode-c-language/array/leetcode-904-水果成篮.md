题目来自于 leetcode 的[904. 水果成篮](https://leetcode-cn.com/problems/fruit-into-baskets/)。

用双指针可以解决该问题，就是需要处理边界问题，和求最小子序列的体型类似。

以下是验证过的源码：

```c
int totalFruit(int* tree, int treeSize){
    int buf[2]; //两棵树的类型
    int max = 0;
    int left = 0;
    int right = 0;
    int count = 1;
    if(treeSize <= 2)
        return treeSize;
    
    buf[0] = tree[0];
    //先找到第二种类型的树
    for (int i=1; i<treeSize; i++)
    {
        if(tree[i] != buf[0])
        {
            buf[1] = tree[i];
            count = i+1;
            break;
        }
    }

    max = count;
    left = 0;
    right = count-1;
    //扫描剩下的树，根据与前面的树类型的情况来选择处理办法
    for (int i=count; i<treeSize; i++)
    {
        if (tree[i] == buf[1])
        {
            count++;
        }
        else if (tree[i] == buf[0])
        {
            buf[0] = buf[1];
            buf[1] = tree[i];
            left = right;
            right = i;
            count++;
        }
        else
        {
            if(count > max) max = count;

            buf[0] = buf[1];
            buf[1] = tree[i];
            left = right;
            right = i;
            
            count = right - left + 1;
        }
    }

    if (count > max) max = count;

    return max;
}
```

