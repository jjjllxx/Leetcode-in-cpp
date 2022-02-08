# 24. Swap Nodes in Pairs
https://leetcode-cn.com/problems/swap-nodes-in-pairs  
Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes 
(i.e., only nodes themselves may be changed.)  

Example 1:  
![image](https://user-images.githubusercontent.com/60777462/153049016-d3cd3e02-d6b9-4594-a29d-8e96ba7108cd.png)  
Input: head = [1,2,3,4]  
Output: [2,1,4,3]  

Example 2:  
Input: head = []  
Output: []  

Example 3:  
Input: head = [1]  
Output: [1]  

Constraints:
The number of nodes in the list is in the range [0, 100].  
0 <= Node.val <= 100  

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
    ListNode* swapPairs(ListNode* head) {
        ListNode* dummy = new ListNode(0);
        dummy->next=head;
        ListNode* p1=dummy;
        while (p1->next && p1->next->next){
            ListNode* one=p1->next->next;
            ListNode* two=p1->next;
            two->next=p1->next->next->next;
            p1->next=one;
            one->next=two;
            p1=p1->next->next;
        }
        return dummy->next;
    }
};
```
