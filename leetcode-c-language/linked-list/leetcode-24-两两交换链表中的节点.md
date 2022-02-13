题目来自于 leetcode 的[24. 两两交换链表中的节点](https://leetcode-cn.com/problems/swap-nodes-in-pairs/)。

难度是中等难度的题目，主要是细节比较多。

#### 我的解法

加个头结点，画画图就好了。

```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */


struct ListNode* swapPairs(struct ListNode* head){
    if ((head == NULL) || (head->next == NULL))
    {
        return head;
    }

    struct ListNode* pre = (struct ListNode*)malloc(sizeof(struct ListNode));
    struct ListNode* preBuf = pre;
    pre->next = head;
    struct ListNode* cur = head;
    struct ListNode* next = head->next;
    head = head->next;
    while (1)
    {
        struct ListNode* temp = next->next;

        pre->next = next;
        next->next = cur;
        cur->next = temp;

        if ((temp == NULL)) break;
        if ((temp->next == NULL)) break;

        pre = cur;
        cur = pre->next;
        next = cur->next;
    }

    preBuf->next = NULL;
    free(preBuf);
    return head;
}
```

