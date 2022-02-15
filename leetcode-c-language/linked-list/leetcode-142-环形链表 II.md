题目来自于 leetcode 的[142. 环形链表 II](https://leetcode-cn.com/problems/linked-list-cycle-ii/)。

#### 我的解法

一道数学题，使用快慢指针，如果两个相遇，即为存在环，然后一个指针从相遇开始，一个指针从头节点开始，相遇的节点即为入口点。数学证明看这篇文章：

https://www.programmercarl.com/0142.环形链表II.html#_142-环形链表ii

```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
struct ListNode *detectCycle(struct ListNode *head) {
    if (head == NULL) return NULL;
    struct ListNode *fast = head;
    struct ListNode *slow = head;

    struct ListNode *index = head;
    while (1)
    {
        slow = slow->next;
        fast = fast->next;
        if (fast == NULL) return NULL;
        fast = fast->next;
        if (fast == NULL) return NULL;

        if (slow == fast)
        {
            break;
        }
    }

    while (1)
    {
        if(slow == index)
        {
            break;
        }
        slow = slow->next;
        index = index->next;
    }

    return index;
}
```

