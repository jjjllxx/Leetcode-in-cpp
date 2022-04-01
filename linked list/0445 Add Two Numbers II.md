# 445. Add Two Numbers II
https://leetcode-cn.com/problems/add-two-numbers-ii/  
You are given two non-empty linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.   
You may assume the two numbers do not contain any leading zero, except the number 0 itself.  

Example 1:  
<img width="530" alt="image" src="https://user-images.githubusercontent.com/60777462/161197921-0f7f15b8-8ffd-4e4b-875b-501f85fc0631.png">  
Input: l1 = [7,2,4,3], l2 = [5,6,4]  
Output: [7,8,0,7]  

Example 2:  
Input: l1 = [2,4,3], l2 = [5,6,4]  
Output: [8,0,7]  

Example 3:  
Input: l1 = [0], l2 = [0]  
Output: [0]  

Constraints:  
The number of nodes in each linked list is in the range [1, 100].  
0 <= Node.val <= 9  
It is guaranteed that the list represents a number that does not have leading zeros.  

Follow up: Could you solve it without reversing the input lists?  

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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        vector<int> nums1, nums2;
        for (ListNode* p1 = l1; p1 != nullptr; p1 = p1->next) {
            nums1.emplace_back(p1->val);
        }
        for (ListNode* p1 = l2; p1 != nullptr; p1 = p1->next) {
            nums2.emplace_back(p1->val);
        }
        if (nums2.size() < nums1.size()) {
            swap(nums1, nums2);
        }
        nums2.insert(nums2.begin(), 0);
        int n = nums2.size(), m = nums1.size(), nxt = 0;
        for (int i = 1; i <= m; i++) {
            nums2[n - i] += nxt + nums1[m - i];
            nxt = nums2[n - i] / 10;
            nums2[n - i] %= 10;
        }
        int pos = n - m - 1;
        while (pos >= 0 && nxt != 0) {
            nums2[pos] += nxt;
            nxt = nums2[pos] / 10;
            nums2[pos] %= 10;
            pos--;
        }
        ListNode* dummy = new ListNode(-1);
        ListNode* p1 = dummy;
        for (int i = (nums2[0] == 0 ? 1 : 0); i < n; ++i) {
            ListNode* cur = new ListNode(nums2[i]);
            p1->next = cur;
            p1 = p1->next;
        }
        return dummy->next;
    }
};
```
