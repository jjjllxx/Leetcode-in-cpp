# 143. Reorder List
https://leetcode-cn.com/problems/reorder-list/  
You are given the head of a singly linked-list. The list can be represented as:  

L0 → L1 → … → Ln - 1 → Ln  
Reorder the list to be on the following form:  

L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …  
You may not modify the values in the list's nodes. Only nodes themselves may be changed.  

Example 1:  
![image](https://user-images.githubusercontent.com/60777462/155174066-55989080-e4d0-40fa-a09e-e3150acfcf1b.png)  
Input: head = [1,2,3,4]  
Output: [1,4,2,3]  

Example 2:  
![image](https://user-images.githubusercontent.com/60777462/155174129-172411fb-74a9-4560-90e0-de942781bbbd.png)  
Input: head = [1,2,3,4,5]  
Output: [1,5,2,4,3]  

Constraints:  
The number of nodes in the list is in the range [1, 5 * 10^4].  
1 <= Node.val <= 1000  

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
    ListNode* myReverse(ListNode* node){
        ListNode* pre=nullptr;
        ListNode* p=node;
        while(p!=nullptr){
            ListNode* tmp=p->next;
            p->next=pre;
            pre=p;
            p=tmp;
        }
        return pre;
    }

    ListNode* middleNode(ListNode* node){
        ListNode *slow=node,*fast=node;
        while(fast->next && fast->next->next){
            fast=fast->next->next;
            slow=slow->next;
        }
        return slow;
    }

    void mergeList(ListNode* l1, ListNode* l2) {
        ListNode* l1_tmp;
        ListNode* l2_tmp;
        while (l1 != nullptr && l2 != nullptr) {
            l1_tmp = l1->next;
            l2_tmp = l2->next;

            l1->next = l2;
            l1 = l1_tmp;

            l2->next = l1;
            l2 = l2_tmp;
        }
    }

    void reorderList(ListNode* head) {
        if(head==nullptr) return;
        ListNode* mid=middleNode(head);
        ListNode* l1=head;
        ListNode* l2=mid->next;
        mid->next=nullptr;
        l2=myReverse(l2);
        mergeList(l1,l2); 
    }
};
```
