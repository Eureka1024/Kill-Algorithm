题目来自于 leetcode 的[[面试题 02.03. 删除中间节点](https://leetcode-cn.com/problems/delete-middle-node-lcci/)](https://leetcode-cn.com/problems/final-value-of-variable-after-performing-operations/)。

#### 我的解法

本来删除单链表的一个节点的操作很简单，只需要知道该节点的前一个节点即可，但是这道题没有给出这个节点，也没有头结点，只给出了要删除的目标节点，按常规思路来说，肯定是实现不了的。

但是考虑到这个节点只有 val 这个元素，我们只需要将当前节点的 val 替换成下一个节点的 val，然后删除下一个节点即可达到相同的目的。

```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
void deleteNode(struct ListNode* node) {
    struct ListNode* nodeNew = NULL;

    node->val = node->next->val;

    nodeNew = node->next;

    node->next = node->next->next;

    free(nodeNew);
}
```

