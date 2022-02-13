题目来自于 leetcode 的[19. 删除链表的倒数第 N 个结点](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)。

难度是中等难度的题目，画图，注意细节。

#### 我的解法

没有使用头结点，处理起来比较复杂，看到别人使用头结点，代码整洁不少。

```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */


struct ListNode* removeNthFromEnd(struct ListNode* head, int n){
    if (head == NULL) return NULL;
    
    int listLen = 0;
    struct ListNode* list = head;
    while (list != NULL)
    {
        list = list->next;
        listLen++;
    }

    if (n > listLen) return head;
    if (n == listLen)
    {
        struct ListNode* temp = head;
        head = head->next;
        free(temp);
        return head;
    }

    list = head;
    for (int i = 1; i < (listLen-n); i++)
    {
        list = list->next;
    }

    struct ListNode* temp = list->next;

    list->next = list->next->next;
    free(temp);

    return head;
}
```

