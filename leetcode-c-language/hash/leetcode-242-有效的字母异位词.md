题目来自于 leetcode 的[242. 有效的字母异位词](https://leetcode-cn.com/problems/valid-anagram/)。

#### 我的解法

没想到这种用数组存储的方式也属于 hash 表的范畴，不过确实是真的好用。

```c
bool isAnagram(char * s, char * t){
    int hash[26] = {0};

    int i = 0;
    while (s[i] != '\0')
    {
       hash[s[i] - 'a']++; 
       i++;
    }

    i = 0;
    while (t[i] != '\0')
    {
       hash[t[i] - 'a']--; 
       i++;
    }

    for (int j = 0; j < 26; j++)
    {
        if (hash[j] != 0)
        {
            return false;
        }
    }

    return true;
}
```

