题目来自于 leetcode 的 [844. 比较含退格的字符串](https://leetcode-cn.com/problems/backspace-string-compare/)。

很容易想到，先把退格的结果求出来，然后比较两个字符串是否相等即可。这样做的坏处是会改变原有字符串的数据，但是题目没说不让改，所以是可行的。

这里使用的是双指针来实现退格处理，看到题解有使用栈，会直观一点，然而我不想额外花时间构建栈。

以下是验证过的源码：

```c
bool backspaceCompare(char * s, char * t){
    int s_size = 0;
    int t_size = 0;
    int i = 0;

    while (s[i] != '\0')
    {
        if(s[i] == '#')
        {
            if (s_size > 0)
                s_size--;
        }
        else
        {
            s[s_size++] = s[i];
        }

        i++;
    }

    i = 0;
    while (t[i] != '\0')
    {
        if(t[i] == '#')
        {
            if (t_size > 0)
                t_size--;
        }
        else
        {
            t[t_size++] = t[i];
        }

        i++;
    }

    if(s_size != t_size)
        return false;

    for(int j=0; j<s_size; j++)
    {
        if (s[j] != t[j])
            return false;
    }

    return true;
}
```

官方也提供了一种用`双指针`实现的方法，能够在不修改原数组的情况下解决该问题。[leetcode 官方题解](https://leetcode-cn.com/problems/backspace-string-compare/solution/bi-jiao-han-tui-ge-de-zi-fu-chuan-by-leetcode-solu/)

代码如下：

```c
bool backspaceCompare(char* S, char* T) {
    int i = strlen(S) - 1, j = strlen(T) - 1;
    int skipS = 0, skipT = 0;

    while (i >= 0 || j >= 0) {
        while (i >= 0) {
            if (S[i] == '#') {
                skipS++, i--;
            } else if (skipS > 0) {
                skipS--, i--;
            } else {
                break;
            }
        }
        while (j >= 0) {
            if (T[j] == '#') {
                skipT++, j--;
            } else if (skipT > 0) {
                skipT--, j--;
            } else {
                break;
            }
        }
        if (i >= 0 && j >= 0) {
            if (S[i] != T[j]) {
                return false;
            }
        } else {
            if (i >= 0 || j >= 0) {
                return false;
            }
        }
        i--, j--;
    }
    return true;
}
```

