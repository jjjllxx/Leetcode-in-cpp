# 82. Remove Duplicates from Sorted List II
https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list-ii  
Given the head of a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list. Return the linked list sorted as well.

Example 1:  
![image](https://user-images.githubusercontent.com/60777462/154483966-424ede4f-5f26-42cd-90a9-2f23009101f9.png)  
Input: head = [1,2,3,3,4,4,5]  
Output: [1,2,5]  

Example 2:  
![image](https://user-images.githubusercontent.com/60777462/154483913-419a030d-78eb-4f25-ba95-43ee5909b7a0.png)  
Input: head = [1,1,1,2,3]  
Output: [2,3]  

Constraints:  
The number of nodes in the list is in the range [0, 300].  
-100 <= Node.val <= 100  
The list is guaranteed to be sorted in ascending order.  

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
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode* dummy=new ListNode(-101);
        dummy->next=head;
        ListNode* fast=head, *slow=dummy;
        while(fast!=nullptr && fast->next!=nullptr){
            if(slow->next->val==fast->next->val){
                while(fast->next!=nullptr && slow->next->val==fast->next->val){
                    fast=fast->next;
                }
                fast=fast->next;
                slow->next=fast;
            } 
            else{
                slow=slow->next;
                fast=fast->next;
            }   
        }
        return dummy->next;
    }
};
```
