题目来自于 leetcode 的[[2114. 句子中的最多单词数](https://leetcode-cn.com/problems/maximum-number-of-words-found-in-sentences/)](https://leetcode-cn.com/problems/final-value-of-variable-after-performing-operations/)。

超级简单，找信心的题目。

#### 我的解法

很简单，数空格即可。

```c
int mostWordsFound(char ** sentences, int sentencesSize){
    int numMax = 0;

    for (int i = 0; i < sentencesSize; i++)
    {
        int j = 0;
        int num = 1;
        while(sentences[i][j] != '\0')
        {
            if (sentences[i][j] == ' ')
            {
                num++;
            }

            j++;
        }

        if (num > numMax) numMax = num;
    }

    return numMax;
}
```

