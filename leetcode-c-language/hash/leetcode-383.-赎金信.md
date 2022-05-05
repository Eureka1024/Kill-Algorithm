题目来自于 leetcode 的[383. 赎金信](https://leetcode-cn.com/problems/ransom-note/)。

#### 我的解法

没想到这种用数组存储的方式也属于 hash 表的范畴，不过确实是真的好用。

```c
bool canConstruct(char * ransomNote, char * magazine){
    int hash[26] = {0};

    int i = 0;
    while (ransomNote[i] != '\0')
    {
       hash[ransomNote[i] - 'a']--; 
       i++;
    }

    i = 0;
    while (magazine[i] != '\0')
    {
       hash[magazine[i] - 'a']++; 
       i++;
    }

    for (int j = 0; j < 26; j++)
    {
        if (hash[j] < 0)
        {
            return false;
        }
    }

    return true;
}
```

