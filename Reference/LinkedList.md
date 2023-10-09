# Linked List

## Definition
``` cpp
struct ListNode
{
    int       val;
    ListNode* next;
    ListNode() :
        val(0), next(nullptr)
    {
    }
    ListNode(int x) :
        val(x), next(nullptr)
    {
    }
    ListNode(int x, ListNode* next) :
        val(x), next(next)
    {
    }
};
```

## Reverse Linked List
``` cpp
ListNode* reverseNode(ListNode* head)
{
    ListNode *cur = head, *pre = nullptr, *nxt;
    while (cur != nullptr)
    {
        nxt       = cur->next;
        cur->next = pre;
        pre       = cur;
        cur       = nxt;
    }

    return pre;
}
```

## Find Middle Node
``` cpp
ListNode* findMiddle(ListNode* head)
{
    ListNode *slow = head, *fast = head;
    while (fast != nullptr && fast->next != nullptr)
    {
        slow = slow->next;
        fast = fast->next->next;
    }

    return slow;
}
```

## Count the Number of Nodes
``` cpp
int countNodes(ListNode* head)
{
    int       cnt = 0;
    ListNode* cur = head;
    while (cur != nullptr)
    {
        cnt++;
        cur = cur->next;
    }

    return cnt;
}
```

## Reminder
1. If it is possible to delete head node, need to create dummy node before head.
2. Fast and slow pointer skill.
3. If need to delete a node, need to know its previous node.