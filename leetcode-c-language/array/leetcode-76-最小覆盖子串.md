题目来自于 leetcode 的[[76. 最小覆盖子串](https://leetcode-cn.com/problems/minimum-window-substring/)](https://leetcode-cn.com/problems/final-value-of-variable-after-performing-operations/)。

不愧是`困难`评级的，确实花了不少时间。

先看看具体的题目内容：

> 给你一个字符串 s 、一个字符串 t 。返回 s 中涵盖 t 所有字符的最小子串。如果 s 中不存在涵盖 t 所有字符的子串，则返回空字符串 "" 。
>
> 注意：
>
> 对于 t 中重复字符，我们寻找的子字符串中该字符数量必须不少于 t 中该字符数量。
> 如果 s 中存在这样的子串，我们保证它是唯一的答案。
>
>
> 示例 1：
>
> 输入：s = "ADOBECODEBANC", t = "ABC"
> 输出："BANC"
>
> 示例 2：
>
> 输入：s = "a", t = "a"
> 输出："a"
> 示例 3:
>
> 输入: s = "a", t = "aa"
> 输出: ""
> 解释: t 中两个字符 'a' 均应包含在 s 的子串中，
> 因此没有符合条件的子字符串，返回空字符串。
>
>
> 提示：
>
> 1 <= s.length, t.length <= 105
> s 和 t 由英文字母组成
>
>
> 进阶：你能设计一个在 o(n) 时间内解决此问题的算法吗？
>
> 来源：力扣（LeetCode）
> 链接：https://leetcode-cn.com/problems/minimum-window-substring
> 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 我的解法

采用暴力破解的方式虽然简单，但是明显不能在o(n) 的时间复杂度内实现。

对于这种找区域最值的题目，很容易想到滑动窗口的方式去实现。

策略是这样的：

1. 设定一个左指针和一个有指针，在初始的情况下都指向开头位置。
2. 然后右指针开始往后移动，直到从左指针到右指针的这段字符串**`满足要求`**。
3. 然后到左指针开始移动，直到从左指针到右指针的这段字符串**`不满足要求`**。
4. 跳转到第二步，继续运行。直到左指针走完，结束。（期间不断记录满足要求的最小值）

对于如何判定字符串是否满足要求，这里有一个很有用的技巧：由于字符串都是字母组成的，而字母的个数是有限的，我们可以设定一个数量为 128 大小的数组num，利用字母的ASIIC码直接定位到数组的具体位置，比如 `num['a']` 显示的是a字母出现的情况。由于题中的 `对于 t 中重复字符，我们寻找的子字符串中该字符数量必须不少于 t 中该字符数量`这个限定，我们先根据 t 的字符串初始化 num，记录每个字母出现的次数。然后当使用上述的滑动窗口策略时，右指针移动时就给对应字母的数量减一，左指针移动时就给对应的字母数量加一，每次检查这个数组的所有成员是否都大于0，若是则说明当前的字符串不满足，反之则满足。

具体的代码实现如下：

```c
//判断当前的字符串是否满足要求
int isSubstring(int num[])
{
    for (int i = 0; i < 128; i++)
    {
        if (num[i] > 0)
        {
            return 0;
        }
    }

    return 1;
}

char * minWindow(char * s, char * t){
    int num[128] = {0};

    int i = 0;
    //根据字符串t的情况，先初始化判断数组
    while (t[i] != '\0')
    {
        num[t[i++]]++;
    }

    int l = 0;
    int r = 0;
    num[s[0]]--;

    int length = strlen(s);
    int direction = 0;//用于切换左右指针的移动
    int target = 0;//记录目标字符串的起始位置，结合min得到最终的字符串
    int min = INT_MAX;//记录最小长度
    while (l < length)
    {
        if (direction == 0) //向右移动
        {
            if (r == length)//右指针到达末端
            {
                direction = 1;//切换到左指针运行
                continue;
            }

            if (isSubstring(num))//目前字符串满足要求
            {
                if ((r - l  + 1) < min)//判断是否最小
                {
                    target = l;
                    min = r - l  + 1;
                }
                direction = 1;//切换到左指针运行
                continue;
            }

            num[s[++r]]--;//对经过的字母的数量进行递减
        }
        else
        {
            num[s[l++]]++;//对经过的字母的数量进行递减增

            if (!isSubstring(num))//目前字符串不满足要求
            {
                direction = 0;//切换到右指针运行
                continue;
            }
            else if ((r - l  + 1) < min)//判断是否最小
            {
                target = l;
                min = r - l  + 1;
            }
        }
    }

    if (min < INT_MAX)
    {
        char* ret = (char*)malloc(sizeof(char) * (min+1));

        for (int i = 0; i < min; i++)
        {
            ret[i] = s[target + i];
        }

        ret[min] = '\0';

        return ret;
    }

    return ""; //不满足条件
}
```

时间复杂度分析：滑动窗口的操作是O(2n)，而判断当前字符串是否为子串的方法是常数次实现，所以最终是满足时间复杂度为 O(n)的要求。

