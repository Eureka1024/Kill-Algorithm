题目来自于 leetcode 的[707. 设计链表](https://leetcode-cn.com/problems/design-linked-list/)。

#### 我的解法

这道题说难不难，就是得注意细节。链表还是很多要注意的地方，很考细节。

```c
typedef struct MyLinkedList1{
    int value;
    struct MyLinkedList1* next;
} MyLinkedList;


MyLinkedList* myLinkedListCreate() {
    MyLinkedList* list = (MyLinkedList*)malloc(sizeof(MyLinkedList));
    list->value = 0;
    list->next = NULL;
    return list;
}

int myLinkedListGet(MyLinkedList* obj, int index) {
    if (index < 0) return -1;

    MyLinkedList* list = obj;

    for (int i = 0; i <= index; i++)
    {
        if (list->next == NULL) return -1;

        list = list->next;
    }

    return list->value;
}

void myLinkedListAddAtHead(MyLinkedList* obj, int val) {
    MyLinkedList* new = (MyLinkedList*)malloc(sizeof(MyLinkedList));
    new->value = val;
    new->next = obj->next;
    obj->next = new;
}

void myLinkedListAddAtTail(MyLinkedList* obj, int val) {
    MyLinkedList* new = (MyLinkedList*)malloc(sizeof(MyLinkedList));
    new->value = val;
    new->next = NULL;

    MyLinkedList* list = obj;
    while(list->next != NULL)
    {
        list = list->next;
    }

    list->next = new;
}

void myLinkedListAddAtIndex(MyLinkedList* obj, int index, int val) {
    if (index < 0) return;

    MyLinkedList* new = (MyLinkedList*)malloc(sizeof(MyLinkedList));
    new->value = val;
    new->next = NULL;

    MyLinkedList* list = obj;
    for (int i = 0; i <= index; i++)
    {
        if (list->next == NULL) 
        {
            if (i == index)
            {
                list->next = new;
            }

            return ;
        }
        list = list->next;
    }

    int tmp = list->value;
    new->next = list->next;
    list->next = new;

    list->value = new->value;
    new->value = tmp;
}

void myLinkedListDeleteAtIndex(MyLinkedList* obj, int index) {
    if (index < 0) return;

    MyLinkedList* list = obj->next;
    MyLinkedList* tmp = obj;
    for (int i = 0; i < index; i++)
    {
        if (list->next == NULL) return;

        list = list->next;
        tmp = tmp->next;
    }

    tmp->next = list->next;
    list->next = NULL;
    free(list);
}

void myLinkedListFree(MyLinkedList* obj) {
    MyLinkedList* tmp = obj;

    while(obj != NULL)
    {   
        tmp = obj;
        obj = obj->next;

        tmp->next = NULL;
        free(tmp);
    }
}

/**
 * Your MyLinkedList struct will be instantiated and called as such:
 * MyLinkedList* obj = myLinkedListCreate();
 * int param_1 = myLinkedListGet(obj, index);
 
 * myLinkedListAddAtHead(obj, val);
 
 * myLinkedListAddAtTail(obj, val);
 
 * myLinkedListAddAtIndex(obj, index, val);
 
 * myLinkedListDeleteAtIndex(obj, index);
 
 * myLinkedListFree(obj);
*/
```

