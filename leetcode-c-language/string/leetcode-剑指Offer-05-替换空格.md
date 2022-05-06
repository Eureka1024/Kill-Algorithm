题目来自于 leetcode 的 [剑指 Offer 05. 替换空格](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/)。



#### 我的解法

其实是使用双指针的一种，通过向后移的操作实现高效率地替换，但是对于C语言，一样设定了新数组，所以从前往后，或者从后往前是一样的。

```c
char* replaceSpace(char* s){
    //统计空格数量
    int spaceCount = 0;
    int len = strlen(s);
    for(int i = 0; i < len; i++)
    {
        if (s[i] == ' ')
        {
            spaceCount++;
        }
    }

    //使用向后移的操作实现替换
    int newLen = len + 1  + spaceCount * 2;
    char* sNew = (char*)malloc(newLen);
    sNew[newLen-1] = '\0';
    int j = newLen - 2;
    for (int i = len - 1; i >= 0; i--)
    {
        if (s[i] == ' ')
        {
            sNew[j--] = '0';
            sNew[j--] = '2';
            sNew[j--] = '%';
        }
        else
        {
            sNew[j--] = s[i];
        }
    }

    return sNew;
}
```

