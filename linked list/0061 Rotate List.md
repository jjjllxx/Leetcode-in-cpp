# 61. Rotate List
https://leetcode-cn.com/problems/rotate-list/   
Given the head of a linked list, rotate the list to the right by k places.   

Example 1:  
<img width="467" alt="image" src="https://user-images.githubusercontent.com/60777462/161198191-631bfccc-1bcc-46e2-8e8d-1bc2e9648780.png">  
Input: head = [1,2,3,4,5], k = 2  
Output: [4,5,1,2,3]  

Example 2:  
<img width="317" alt="image" src="https://user-images.githubusercontent.com/60777462/161198229-7d809831-7230-450c-96af-29c1e74dfa59.png">  
Input: head = [0,1,2], k = 4  
Output: [2,0,1]  

Constraints:  
The number of nodes in the list is in the range [0, 500].  
-100 <= Node.val <= 100  
0 <= k <= 2 * 10^9  

``` cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* rotateRight(ListNode* head, int k) {
        if (head == nullptr) {
            return head;
        }
        int n = 0;
        for (ListNode* p = head; p != nullptr; p = p->next) {
            n++;
        }
        k = k % n;
        if (k == 0) {
            return head;
        }
        k = n - k - 1;
        ListNode* pos = head;
        while(k--) {
            pos = pos->next;
        }
        ListNode* newHead = pos->next, *nxt = newHead;
        pos->next = nullptr;
        while(nxt->next != nullptr) {
            nxt = nxt->next;
        }
        nxt->next = head;
        return newHead;
    }
};
```
